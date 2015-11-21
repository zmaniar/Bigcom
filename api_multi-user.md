# <a name="intro"></a>Introduction

When you register your app with Bigcommerce, if you [enable multi-user support](/api/registration#multiuser), it will allow store admins to manually authorize users other than the store owner to load the app. This feature is not available for [Private Apps](/api/legacy/basic-auth).

# Enable multi-user support

As soon as you [enable multi-user support](/api/registration#multiuser), it affects the Control Panel of any store with your app installed. If you already have an app published in the App Store, be mindful that this setting takes affect immediately. We recommend testing your multi-user support using a separate app in Draft status.

>PRO TIP: Let your customers know that you've enabled this feature! Otherwise, they won't know that they can start granting access to users.</span></div>

To opt in:

1.  Log into [**My Apps**](https://developer.bigcommerce.com/auth/bigcommerce).
2.  In the **Technical** panel, select **Multiple Users** in the **Supported Features** area.
3.  Provide a **Remove User Callback URI** in the **Remove User Callback URI** box.
4.  Save and close your app.

# About the control panel experience

Store admins will be able to adjust user permissions to grant/deny access to your app for other store users.

The next time the user logs in, they will see any apps for which they have been granted access. The user can then click on the app icon in the left navigation to load it.

Use your draft app and your sandbox store to review this behavior.

# About the load request

Apps with multiple users enabled can expect more than just the store owner's email and ID in the JSON object sent in the load request. If a load request is sent with user information you haven't seen yet, you should provision the user account and associate it with the store in your database.

Because you know the store owner's email and ID from the [App Installation](/api/callback) sequence, your app can distinguish store owners from other users. This allows you to provide different user experiences based on the information in the load request. A summary of the two types of users follows.

*   **Store owner**: can install, uninstall, and load apps.
*   **Users**: cannot install or uninstall apps. Only allowed to load the apps that a store admin has authorized.

Review [Processing Load, Uninstall, and User Removal Requests](/api/load) for more information.

# About the remove user request

In addition to the ability to add users, store admins can also remove users. This action results in a `**GET**` request to the **Remove User Callback URI** that you provided in **My Apps**. Your app should delete the user identified in the request from its records.

Review [Processing Load, Uninstall, and User Removal Requests](/api/load) for more information.
