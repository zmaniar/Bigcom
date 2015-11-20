##Response Headers

<table class="bui-table">

<thead>

<tr>

<th class="headers-name">Header</th>

<th class="headers-values">Possible Values</th>

<th class="headers-description">Description</th>

<th class="headers-example">Example</th>

</tr>

</thead>

<tbody>

<tr>

<td>

`**Date**`

</td>

<td>

An [RFC 2822](http://tools.ietf.org/html/rfc2822#section-3.3) date.

</td>

<td>

The date the response was sent.

</td>

<td>

`**Tue, 15 Nov 2011 12:45:26 GMT**`

</td>

</tr>

<tr>

<td>

`**Last-Modified**`

</td>

<td>

An [RFC 2822](http://tools.ietf.org/html/rfc2822#section-3.3) date.

</td>

<td>

The date the resource was last modified. Please refer to the individual resource pages for support for this header.

</td>

<td>

`**Tue, 15 Nov 2011 12:45:26 GMT**`

</td>

</tr>

<tr>

<td>

`**Content-Type**`

</td>

<td>

`**application/json**` (for JSON requests) `**application/xml**` (for XML requests, or if no extension is supplied)

</td>

<td>

The MIME type of the response, dependent on the extension of the endpoint that was requested.

</td>

<td>

`**application/json**`

</td>

</tr>

<tr>

<td>

`**Content-Location**`

</td>

<td>

A URI.

</td>

<td>

Sent if the request was redirected.

</td>

<td>

`**/api/v2/orders/5.json**`

</td>

</tr>

<tr>

<td>

`**WWW-Authenticate**`

</td>

<td>

`**Basic**`

</td>

<td>

Indicates the authentication scheme that should be used to access the API. Sent with a `**401 Unauthorized**` response if HTTP Basic Authentication credentials weren’t supplied.

</td>

<td>

`**Basic**`

</td>

</tr>

<tr>

<td>

`**Location**`

</td>

<td>

A URI

</td>

<td>

The URI of a newly created resource. Sent with a `**201 Created**` response.

</td>

<td>

`**/api/v2/products/7**`

</td>

</tr>

<tr>

<td>

`**X-Retry-After**`

</td>

<td>

An integer

</td>

<td>

Rate limited response, indicating the number of seconds before the quota refreshes. See the [OAuth rate limits documentation](/api/rate-limits/oauth) for more information.

</td>

<td>

`**15**`

</td>

</tr>

<tr>

<td>

`**X-BC-ApiLimit-Remaining**`

</td>

<td>

An integer

</td>

<td>

The number of API requests remaining for the current period (rolling one hour). See the [Basic Auth rate limits documentation](/api/rate-limits/basic) for more information.

</td>

<td>

`**987**`

</td>

</tr>

<tr>

<td>

`**X-BC-Store-Version**`

</td>

<td>

A version number

</td>

<td>

The version of Bigcommerce the store is running on. This header is available from versions 7.3.6+.

</td>

<td>

`**7.3.6**`

</td>

</tr>

</tbody>

</table>

</div>

</div>
