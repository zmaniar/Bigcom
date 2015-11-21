## OAuth Scopes

The following table identifies the name used for each OAuth scope in the My Apps and Control Panel GUI and what it corresponds to in terms of resources and the strings that get passed to your app during [app installation](/api/callback).

All OAuth scopes except `**default**` have `**read_only**` scopes which allow only `**GET**` and `**HEAD**` requests.

<table class="bui-table"><colgroup><col style="width:33.333%"> <col style="width:33.333%"> <col style="width:33.333%"></colgroup>

<thead>

<tr>

<th>Scope GUI Name</th>

<th>Scope Strings</th>

<th>Resources</th>

</tr>

</thead>

<tbody>

<tr>

<td>Content</td>

<td>`**store_v2_content**`  
`**store_v2_content_read_only**`</td>

<td>[blog/posts](/api/stores/v2/blog/posts)  
[blog/tags](/api/stores/v2/blog/tags)  
[redirects](/api/stores/v2/redirects)</td>

</tr>

<tr>

<td>Customers</td>

<td>`**store_v2_customers**`  
`**store_v2_customers_read_only**`</td>

<td>[customers](/api/stores/v2/customers)  
[customers/{id}/addresses](/api/stores/v2/customers/addresses)  
[customer_groups](/api/stores/v2/customer_groups)</td>

</tr>

<tr>

<td>Default</td>

<td>`**default**`</td>

<td>[countries](/api/stores/v2/countries)  
[countries/{id}/states](/api/stores/v2/countries/states)  
[hooks](/api/stores/v2/webhooks)  
[time](/api/stores/v2/time)</td>

</tr>

<tr>

<td>Information</td>

<td>`**store_v2_information**`  
`**store_v2_information_read_only**`</td>

<td>[payments/methods](/api/stores/v2/payments/methods)  
[shipping/methods](/api/stores/v2/shipping/methods)  
[store](/api/stores/v2/store_information)  
[tax_classes](/api/stores/v2/tax_classes)</td>

</tr>

<tr>

<td>Marketing</td>

<td>`**store_v2_marketing**`  
`**store_v2_marketing_read_only**`</td>

<td>[coupons](/api/stores/v2/coupons)</td>

</tr>

<tr>

<td>Orders</td>

<td>`**store_v2_orders**`  
`**store_v2_orders_read_only**`</td>

<td>[orders](/api/stores/v2/orders)  
[orders/{id}/coupons  
](/api/stores/v2/orders/coupons)[orders/{id}/messages  
](/api/stores/v2/orders/messages)[orders/{id}/products  
](/api/stores/v2/orders/products)[orders/{id}/shipping_addresses  
](/api/stores/v2/orders/shipping_addresses)[orders/{id}/order_statuses  
](/api/stores/v2/order_statuses)[orders/{id}/taxes  
](/api/stores/v2/orders/taxes)[orders/{id}/shipments](/api/stores/v2/orders/shipments)</td>

</tr>

<tr>

<td>Products</td>

<td>`**store_v2_products**`  
`**store_v2_products_read_only**`</td>

<td>[brands](/api/stores/v2/brands)  
[products/{id}/discount_rules  
](/api/stores/v2/products/discount_rules)[categories  
](/api/stores/v2/categories)[products/{id}/configurable_fields  
](/api/stores/v2/products/configurable_fields)[products/{id}/custom_fields  
](/api/stores/v2/products/custom_fields)[products/{id}/googleproductsearch  
](/api/stores/v2/products/googleproductsearch)[options  
](/api/stores/v2/options)[option_sets  
](/api/stores/v2/option_sets)[option_sets/{id}/options  
](/api/stores/v2/option_sets/options)[options/{id}/values  
](/api/stores/v2/options/values)[products  
](/api/stores/v2/products)[products/{id}/images  
](/api/stores/v2/products/images)[products/{id}/options  
](/api/stores/v2/products/options)[products/{id}/reviews  
](/api/stores/v2/products/reviews)[products/{id}/rules  
](/api/stores/v2/products/rules)[products/{id}/videos  
](/api/stores/v2/products/videos)[products/{id}/skus](/api/stores/v2/products/skus)</td>

</tr>

</tbody>

</table>
