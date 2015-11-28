## Introduction

Our submission guidelines aim to protect the merchant experience, as well as provide enough structure for you to develop apps efficiently and effectively.

## App Requirements

*   Must perform as described.

*   All information supplied as part of the app submission process must be genuine and accurate.

*   Must provide pricing information including pricing for starting a new service and the cost of services after the free trial.

*   All API requests must be made using OAuth authentication.

*   Must be production ready and free of defects.

<div class="bui-message bui-message-info"><span class="bui-message-text">PRO TIP: Install and test your app thoroughly prior to submission. Be sure to install and run your app inside of your sandbox store as a draft to conduct your tests.</span></div>

*   Must function properly on all [supported browsers](/api/browsers) and conform to the [user interface constraints](/api/ui-constraints), such as P3P policies as necessary and no mixed content.

*   The entire app should operate within the iframe that opens when the user clicks on your app icon in the launch bar of the Control Panel. Exceptions may be made for apps that need to authenticate to other services using OAuth—as long as they open a new tab to do so.

*   Must be easy to use.

*   Whenever possible, use the API resources to auto-fill and obtain information rather than prompting the user. Apps requesting information that can be auto-filled will be rejected.

<div class="bui-message bui-message-info"><span class="bui-message-text">PRO TIP: The store name, phone number, and other information can be obtained from the [Store Information](/api/store) resource.</span></div>

*   The user ID and email address from the [OAuth flow](/api/load#process) should allow you to log the merchant into any additional systems automatically. Apps that provide the merchant with a single sign-on experience are preferred.

*   Must return some HTML in response to GET requests to the [Auth Callback URI](/api/load#process).

*   Must use a TLS/SSL certificate signed by a valid certificate authority. Self-signed certificates will generate browser warnings and are not acceptable.

*   No competitor integrations or references should appear in app or in marketing materials.

*   Any instances of the Bigcommerce brand name must be correctly spelled, i.e., one word with a lowercase 'c'.

*   Must have all required information and files discussed in [App Submission](/api/completing-reg).

## Types of apps we're accepting

| Accepting | Not accepting |
| --- | --- |
| Accounting | Real-Time Tax |
| Advertising | Customized Checkout |
| Analytics | Real-time Shipping Rate updates |
| Cloud integration | Payment Methods |
| Customer feedback |
| Drop shipping |
| Email marketing |
| Live chat |
| Marketing |
| Merchandising |
| Mobile |
| Multichannel listing |
| Order fulfillment |
| Order management |
| Point of sale |
| Product review |
| Shipping |
| Shopping comparison |
| Social media |
| Split testing |

Questions? Please contact [appstore@bigcommerce.com](mailto:appstore@bigcommerce.com)
