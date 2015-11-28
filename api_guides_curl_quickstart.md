## Introduction

This page provides some sample cURL commands for quick start purposes. These use Basic Authentication. Before you can issue them, you must generate Basic Authentication credentials following the steps discussed in the [Overview](/api/legacy/basic-auth). Once you have your Basic Authentication credentials, you can issue cURL commands as shown below.

**curl --request GET \
    -H "Authorization: Basic _username_:_API_key_" \
    https://store.mybigcommerce.com/api/v2/time** 

If the request is made using **Authorization** header, you need to encode the credentials using base64\. Or a simple way to do the same thing as above is:

<pre class=“pretty print”>curl --request GET \
    -u "_username_:_API_key_" \
    https://store.mybigcommerce.com/api/v2/orders.json</pre>

## Orders

### Get a list of orders from the store

<pre class=“pretty print”>curl --request GET \
    -u "_username_:_API_key_" \
    https://store.mybigcommerce.com/api/v2/orders.json</pre>

By default, the api request returns only 50 orders. If you want to return all the orders from the store, you have to use filters. Look at the example below.

<a name="Get.all.orders.from.the.store"></a>

### Get all orders from the store

Use the **limit** and **page** filter parameters to get a data beyond what the default query returns. Note that, per page, 200 orders is the max returned.

<pre class=“pretty print”>curl --request GET \
    -u "_username_:_API_key_" \
    https://store.mybigcommerce.com/api/v2/orders.json?limit=200&page=1</pre>

<a name="Update.an.order"></a>

### Update an order

Order takes many fields on the update requests. Refer to the documentation [here](http://developer.bigcommerce.com/api/orders#put-ordersidjson). Here, we update an order using just the mandatory fields.

<pre class=“pretty print”>curl --request PUT \
    -u "_username_:_API_key_" \
    -H "Content-Type: application/json" \
    --data-binary '{"status_id":1}' \
    https://store.mybigcommerce.com/api/v2/orders/101</pre>

<a name="Get.orders.created.since.a.date"></a>

### Get orders created since a date

You can use the **'If-Modified-Since'** header to request orders that have been created after a date.

<pre class=“pretty print”>curl -I --request GET \
    -u "_username_:_API_key_" \
    -H "Content-Type: application/json" \
    -H "If-Modified-Since: Tue, 4 Dec 2012 00:00:00 GMT" \
    https://store.mybigcommerce.com/api/v2/orders.json</pre>

<a name="Get.coupons.associated.with.an.order"></a>

### Get coupons associated with an order

An order can contain coupons applied to it. This might provide discounts to the customer. You can look at all the available coupons in an order as follows:

<pre class=“pretty print”>curl --request GET \
    -u "_username_:_API_key_"\
    https://store.mybigcommerce.com/api/v2/orders/115/coupons.json</pre>

<a name="Create.a.shipment.for.an.order"></a>

### Create a shipment for an order

One can create a shipment for an order via the orders/shipment endpoint. As an example, third-party shipping services can query orders from a store when they are created and create shipments for those.

<pre class=“pretty print”>curl --request POST \
    -u "_username_:_API_key_" \
    -H "Content-Type: application/json" \
    -d '{"order_address_id":15,"tracking_number":"123-123-123","items":[{"order_product_id":15,"quantity":1}]}' \
    https://store.mybigcommerce.com/api/v2/orders/114/shipments.json</pre>

## Products

### Get a list of products from the store

<pre class=“pretty print”>curl --request GET \
    -u "_username_:_API_key_" \
    https://store.mybigcommerce.com/api/v2/products.json</pre>

By default, the API request returns only 50 products. If you want to return all the products from the store, you have to use filters. Look at the example below.

<a name="Get.all.products.from.the.store"></a>

### Get all products from the store

Use the **limit** and **page** filter parameters to get a data beyond what the default query returns. Note that 200 products is the max returned per page.

<pre class=“pretty print”>curl --request GET \
    -u "_username_:_API_key_" \
    https://store.mybigcommerce.com/api/v2/products.json?limit=200&page=1</pre>

<a name="Create.a.product"></a>

### Create a product

Products have many fields. You can check out [this docs page](http://developer.bigcommerce.com/api/products#post-productsjson) for information on the product fields allowed as part of a POST request.

Let us say, we want to create a product using just the mandatory fields needed for a POST request. Note that price needs to specified as a string, while the weight is a decimal. Note that if the **is_visible** flag, though not mandatory is not set to **true**, the product by default would not be visible -

<pre class=“pretty print”>curl --request POST \
    -H "Content-Type: application/json" \
    -u "_username_:_API_key_" \
    -d '{"name":"startrek","price":19.99,"categories":[2],"type":"physical","availability":"available", "weight":0}' \
    https://store.mybigcommerce.com/api/v2/products.json</pre>

<a name="Update.a.product"></a>

### Update a product

To update the product created above, you can use the following:

<pre class=“pretty print”>curl --request PUT \
    -H "Content-Type: application/json" \
    -u "_username_:_API_key_" \
    -d '{"name":"startrek","sku":"STREK-DVD","categories":[2,3],"inventory_tracking":"simple","inventory_level":"500", "inventory_warning":100}' \
    https://store.mybigcommerce.com/api/v2/products/id.json</pre>

<a name="Search.a.product.by.SKU"></a>

### Search a product by SKU

If we want to search by a product SKU, we can use the following code. Remember that when a product has optionset/variations defined, and if the individual options have SKUs defined, then the product SKU is overriden by the option SKUs. Currently, there are two ways to search for SKUs - **GET /products?sku="something"** or **GET /products/skus?sku="something"**. The first call only returns product level SKU and not option level SKUs.

<pre class=“pretty print”>curl --request GET \
    -u "_username_:_API_key_" \
    https://store.mybigcommerce.com/api/v2/products/skus.json?sku="abcd"</pre>

## Coupons

### Get a list of coupons from the store

<pre class=“pretty print”>curl --request GET \
    -u "_username_:_API_key_" \
    https://store.mybigcommerce.com/api/v2/coupons.json</pre>

Coupons can be filtered through **code**, **type**, **name**, **min_id** and **max_id**. Without these filters, the call returns all the coupons in the store. For instance, if we want to return a list of coupons that are of type **percentage_discount**, we can request the results using the following.

<pre class=“pretty print”>curl --request GET \
    -u "_username_:_API_key_" \
    https://store.mybigcommerce.com/api/v2/coupons.json?type=percentage_discount</pre>

Refer to the [Coupons resource](/api/stores/v2/coupons) for the filtering field.

<a name="Create.a.coupon"></a>

### Create a coupon

Coupons can be created by a **POST** request on the coupons endpoint. For example, if we want to create a coupon to take 50% off an order, then our coupon will have **percentage_discount** as the type. The **applies_to** field is optional and can be used to restrict the coupon to a set of products or categories. In the example shown below, the coupon is being restricted to a set of products.

<pre class=“pretty print”>curl --request POST \
    -H "Content-Type: application/json" \
    -u "_username_:_API_key_" \
    -d '{"code":"50OFF", "type":"percentage_discount", "name":"testcoupon1", "amount":50.00, "enabled":"true", "applies_to":"{\"entity\":\"products\",\"ids\":[32]}"}' \
    https://store.mybigcommerce.com/api/v2/coupons.json</pre>

<a name="Update.a.coupon"></a>

### Update a coupon

Updating a coupon is almost similar to above, except that we work off an ID via a **PUT** request. For example, if we want to change the above coupon to a 30% discount instead of 50%, and say, the coupon ID is 15, we can update the coupon using the following.

<pre class=“pretty print”>curl --request PUT \
    -H "Content-Type: application/json" \
    -u "_username_:_API_key_" \
    -d '{"code":"30OFF", "type":"percentage_discount"' \
    https://store.mybigcommerce.com/api/v2/coupons/15.json</pre>

## Option Sets

### Connect options to option sets

This is currently a four step process.

1.  Create the option.
2.  Add some values to the option.
3.  Create the option set.
4.  Create option set options using the options you just created.

Use the following command to create an option.

<pre class=“pretty print”>curl --request POST \
    -H "Content-Type: application/json" \
    -u "_username_:_API_key_" \
    -d '{"name":"homer simpson", "type":"T"}' \
    https://store.mybigcommerce.com/api/v2/options.json</pre>

Bigcommerce returns the following, which includes an option ID.

<pre class=“pretty print”>{"id":33,"name":"homer simpson","display_name":"homer simpson","type":"T","values":{"url":"https://store.mybigcommerce.com-bwvr466.mybigcommerce.com/api/v2/options/33/values.json","resource":"/options/33/values"}}</pre>

Next, create a new option set.

<pre class=“pretty print”>curl --request POST \
    -u "admin:key" \
    -d '{"name": "Simpson family"}' \
    -H "Content-Type: application/json" \
    https://store.mybigcommerce.com/api/v2/optionsets.json</pre>

The API returns the following, which includes an option set ID.

<pre class=“pretty print”>{"id":27,"name":"Simpson family","options":{"url":"https://store.mybigcommerce.com-bwvr466.mybigcommerce.com/api/v2/optionsets/27/options.json","resource":"/optionsets/27/options"}}</pre>

The final step is to connect the option with the option set.

<pre class="pretty print">**curl --request POST \
    -u "_username_:_API_key_" \
    -d '{"option_id": "33", "display_name":"Simpson family"}' \
    -H "Content-Type: application/json" \
    https://store.mybigcommerce.com/api/v2/optionsets/27/options.json</pre>

Which results in the following.

<pre class="pretty print">**{"id":44,"option_id":33,"option_set_id":27,"display_name":"Simpson family","sort_order":0,"is_required":false,"option":{"url":"https://store.mybigcommerce.com-bwvr466.mybigcommerce.com/api/v2/options/33.json","resource":"/options/33"}}</pre>
