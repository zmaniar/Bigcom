## Introduction

In addition to the **Auth Callback URI**, the [App Registration](/api/registration) wizard requests the following URIs.

<table class="bui-table">

<thead>

<tr>

<th>Name</th>

<th>Required?</th>

<th>Event Discussion</th>

</tr>

</thead>

<tbody>

<tr>

<td>**Load Callback URI**</td>

<td>Yes</td>

<td>Called when the store owner or user clicks to load your app.</td>

</tr>

<tr>

<td>**Uninstall Callback URI**</td>

<td>No</td>

<td>Called when the store owner clicks to uninstall your app.</td>

</tr>

<tr>

<td>**Remove User Callback URI**</td>

<td>No</td>

<td>Called when the store admin revokes a user's access to your app.</td>

</tr>

</tbody>

</table>

Each Bigcommerce request is a `**GET**` request and includes a signed payload that allows your app to:

*   Verify that the request came from Bicommerce.
*   Identify the store.
*   Identify the store owner or user.

The remainder of this page discusses:

*   [The load request and response](#load).
*   [The uninstall request](#uninstall).
*   <a href="">The remove user request</a>.
*   [The signed payload.](#process)

## About the load request and response

Once your app has been installed, the store owner or user can click its icon in the Control Panel to launch it. This causes Bigcommerce to send a `**GET**` request to the **Load Callback URI** that you provided. In a production environment, the **Load Callback URI** must be publicly available, fully qualified, and served over TLS/SSL.

<div class="bui-message bui-message-info"><span class="bui-message-text">PRO TIP: The load request comes from the client browser, rather than directly from Bigcommerce. This allows you to use a non-publicly-available **Load Callback URI** while testing your app.</span></div>

The `**GET**` request contains a signed payload, as shown below.

    GET /load?signed_payload=hw9fhkx2ureq.t73sk8y80jx9 HTTP/1.1
    Host: app.example.com

Upon receiving a `**GET**` request to the **Load Callback URI**, your app needs to [process the signed payload](#process).

After processing the payload, your app returns its user interface as HTML. Bigcommerce renders this inside of an iframe. Please see [User Interface Constraints](/api/ui-constraints) for important information about your app's user interface.

## About the uninstall request (optional)

Store owners have the option to uninstall any app at any time. When a store owner uninstalls an app, the app's OAuth token is revoked and the app cannot make requests to the Stores API on the store's behalf anymore.

You do not need to provide an **Uninstall Callback URI**. The lack of an **Uninstall Callback URI** does not prevent uninstallation. Instead, the **Uninstall Callback URI** allows you to track store owners who uninstall your app and to run cleanup operations, such as removing the store's user accounts from your system.

Should you choose to avail of this option and provide an **Uninstall Callback URI**, please note that it must be publicly available, fully qualified, and served over TLS/SSL. If provided, Bigcommerce will send a `**GET**` request to your **Uninstall Callback URI** when a store owner clicks to uninstall your app. An example follows.

    GET /uninstall?signed_payload=hw9fhkx2ureq.t73sk8y80jx9 HTTP/1.1
    Host: app.example.com

Upon receiving the `**GET**` request, your app will need to [process the signed payload](#process).

<div class="bui-message bui-message-info"><span class="bui-message-text">PRO TIP: Any HTML that you return in your response will not be rendered.</span></div>

## About the remove user request (optional)

If you have not enabled [multi-user support](/api/multi-user), you will not provide a **Remove User Callback URI** and can ignore this section. If you enable multi-user support, you can optionally specify a **Remove User Callback URI**. It must be fully qualified, publicly available, and served over TLS/SSL. Bigcommerce will send a `**GET**` request to your **Remove User Callback URI** when a store admin revokes a user's access to your app. An example follows.

    GET /remove-user?signed_payload=hw9fhkx2ureq.t73sk8y80jx9 HTTP/1.1
    Host: app.example.com

Upon receiving the `**GET**` request, your app will need to [process the signed payload](#process).

<div class="bui-message bui-message-info"><span class="bui-message-text">PRO TIP: Any HTML that you return in your response will not be rendered.</span></div>

## Processing the signed payload

### Splitting and decoding the signed payload

The signed payload is a string containing a base64url-encoded JSON string and a base64url-encoded [HMAC signature](http://en.wikipedia.org/wiki/Hash-based_message_authentication_code). The parts are delimited by the `**.**` character:

    encoded_json_string.encoded_hmac_signature

To decode the signed payload, complete the following steps:

1.  Split `**signed_payload**` into its two parts at the `**.**` delimiter.
2.  Decode `**encoded_json_string**` using base64url.
3.  Convert the decoded JSON string into an object. See [Processing the JSON object](#Identifying) in for more about this object.
4.  Decode `**encoded_hmac_signature**` using base64url.
5.  Use your client secret to verify the signature. See the next section for more details.

### Verifying the HMAC signature

To verify the payload, you need to sign the payload using your client secret, and confirm that it matches the signature that was sent in the request.

<div class="bui-message bui-message-info"><span class="bui-message-text">PRO TIP: To limit the vulnerability of your app to [timing attacks](http://codahale.com/a-lesson-in-timing-attacks/), we recommend using a constant time string comparison function rather than the equality operator to check that the signatures match.</span></div>

#### Examples

<div class="bui-tabs">

*   [PHP](#strcmp-php)
*   [Ruby](#strcmp-ruby)

<div class="bui-tab-panel is-active" id="strcmp-php">

    function verifySignedRequest($signedRequest)
    {
    	list($encodedData, $encodedSignature) = explode('.', $signedRequest, 2); 

    	// decode the data
    	$signature = base64_decode($encodedSignature);
            $jsonStr = base64_decode($encodedData);
    	$data = json_decode($jsonStr, true);

    	// confirm the signature
    	$expectedSignature = hash_hmac('sha256', $jsonStr, $clientSecret(), $raw = false);
    	if (!hash_equals($expectedSignature, $signature)) {
    		error_log('Bad signed request from Bigcommerce!');
    		return null;
    	}
    	return $data;
    }

<div class="bui-message bui-message-info"><span class="bui-message-text">NOTE: `**!hash_equals**` is available in PHP 5.6 and later. If you are running an older version of PHP, pull in a compatibility library such as the following: [https://packagist.org/packages/realityking/hash_equals](https://packagist.org/packages/realityking/hash_equals). The [hello-world-app-php-silex app](https://github.com/bigcommerce/hello-world-app-php-silex) sample app from Bigcommerce does this automatically.</span></div>

</div>

<div class="bui-tab-panel" id="strcmp-ruby">

    require "base64"
    require "openssl"

    def verify(signed_payload, client_secret)
      message_parts = signed_payload.split(".")

      encoded_json_payload = message_parts[0]
      encoded_hmac_signature = message_parts[1]

      payload_object = Base64.strict_decode(encoded_json_payload)
      provided_signature = Base64.strict_decode(encoded_hmac_signature)

      expected_signature = OpenSSL::HMAC::hexdigest("sha256", client_secret, payload_object)

      return false unless secure_compare(expected_signature, provided_signature)

      JSON.parse(payload_object)
    end

    def secure_compare(a, b)
      return false if a.blank? || b.blank? || a.bytesize != b.bytesize
      l = a.unpack "C#{a.bytesize}"

      res = 0
      b.each_byte { |byte| res |= byte ^ l.shift }
      res == 0
    end

</div>

</div>

### Processing the JSON object

#### Introduction

The JSON object embedded in the `**signed_payload**` contains information about the Bigcommerce store and the store owner or user.

#### Identifying the store

You should use the store information to identify the store that the request pertains to.

#### Interpreting the user information

Interpreting the user information varies as follows.

<table class="bui-table">

<thead>

<tr>

<th>Request type</th>

<th>Multiple users enabled</th>

<th>Multiple users not enabled</th>

</tr>

</thead>

<tbody>

<tr>

<td>Load</td>

<td>Compare the user information to see if it matches that of the store owner, received at the time of [App Installation](/api/callback) or that of an existing user. If the user information does not match either of these, then it represents a new user that you should add to your database or other storage.</td>

<td>The information should match that of the store owner, received at the time of [App Installation](/api/callback).</td>

</tr>

<tr>

<td>Uninstall</td>

<td>The user information should match that of the store owner. Only the store owner can uninstall your app.</td>

<td>Should match the store owner.</td>

</tr>

<tr>

<td>Remove user</td>

<td>The user information should match one of the users that you have stored. After locating the stored user, delete it from your database or other storage.</td>

<td>N/A</td>

</tr>

</tbody>

</table>

#### JSON Values

<table class="bui-table">

<thead>

<tr>

<th>Name</th>

<th>Data Type</th>

<th>Value Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>`**id**`</td>

<td>integer</td>

<td>Unique identifier for the user.</td>

</tr>

<tr>

<td>`**email**`</td>

<td>string</td>

<td>The user’s email address.</td>

</tr>

<tr>

<td>`**store_hash**`</td>

<td>string</td>

<td>Unique identifier of the store.</td>

</tr>

</tbody>

</table>

#### JSON Example

    {
      "user": {
    	"id": 24654,
    	"email": "user@mybigcommerce.com"
      },
      "store_hash": "g5cd38"
    }
