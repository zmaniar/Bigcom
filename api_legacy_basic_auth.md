## Introduction

Private apps require the manual creation of an API token for each store, and are most useful for custom integrations for a single Bigcommerce store. They use HTTP Basic Authentication, and communicate directly with the store's API endpoints.

<div class="bui-message bui-message-info"><span class="bui-message-text">PRO TIP: Not all features of the Stores API are available to apps using Basic Authentication. For example, the webhooks resource requires OAuth.</span></div>

## Making requests

To allow an app to connect to a store using Basic Authentication, the store owner must manually generate an API key and provide this to the app developer along with a base path and user name.

To connect to a store using Basic Authentication, an app must:

*   Include the user name and API key in the `**Authorization**` field of each HTTP request header, using the following syntax `**Basic _username:API_key_**`, where `**_username:API_key_**` is base64-encoded. An example follows.
    `**Authorization: Basic YWRtaW46ZTBhMDJiMDM5NzczNWI4NzNlZGQ5NWE1ZmQ1Y2I5YmI=**`

*   Use the base path provided by the store owner.

*   Use TLS encryption.

If the user name and/or API token are invalid or missing, the app will get a `**401 Unauthorized**` response.

## Obtaining an API token

To get an API token, complete the following steps.

1.  Log into the store.
2.  Click **Setup & Tools**.
3.  Select **Legacy API Accounts**.
4.  Click **Create a Legacy API Account**.
5.  Type the name of the user in the **Username** box.
6.  Copy the contents of the **API Path** box and paste this value into a text editor.
7.  Copy the contents of the **API Token** box and paste this value into a text editor.
8.  Click the **Save** button.
9.  Provide the user name, API base path, and API token to the app developer using a secure channel.

## Revoking app access

To revoke app access to a store, complete the following steps.

1.  Log into the store.
2.  Click **Setup & Tools**.
3.  Select **Legacy API Accounts**.
4.  Click the gears icon in the **Action** column and select **Edit**.
5.  Click the **Generate New Token** button.
6.  Select the **Save** button.
7.  Select the check box next to the user.
8.  Click the trash can button.
9.  Click **OK** in the confirmation prompt.

## Regenerating an API token

To change the API token that an app is using to access a store, complete the following steps.

1.  Log into the store.
2.  Click **Setup & Tools**.
3.  Select **Legacy API Accounts**.
4.  Click the gears icon in the **Action** column and select **Edit**.
5.  Click the **Generate New Token** button.
6.  Select the **Save** button.
