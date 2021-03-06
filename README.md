<h1 align="center"> Simple Cart Service </h1>

Simple cart service built using [Lumen](https://lumen.laravel.com/).

This service emulates a third party Shopping cart service that can be called by client applications that have applied for an API key.

## Running locally and testing

In order to run the service, clone the repo to a server that meets the [server requirements](https://lumen.laravel.com/docs/8.x#server-requirements) and set your document root to the **public** folder. By default the service uses SQLite for storage

## API

### Get an API key

<hr>
In order to use the cart service, you'd first need to make `POST` request to `/key` to get an API key. You need to provide two fields namely:

-   name
-   email

```
curl --location --request POST 'http://localhost/key' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'name=Testing' \
--data-urlencode 'email=demo@test.com'
```

Response will be a 32 character API key. Every request to the cart API need to include a `x-api-key` header with your API key.

### Create Cart

<hr>

To create a cart pass all you need to is pass the `customer_id` form field, which is an ID generated by the third party system in order to identify a customer in the cart system.

```
curl --location --request POST 'http://localhost/carts' \
--header 'x-api-key: <YOUR_API_KEY>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'customer_id=<YOUR_GENERATED_KEY>'
```

### Get Cart

Returns your cart object, including all associated cart items.

```
curl --location --request GET 'http://localhost/cartitems/<CART_ID>' \
--header 'x-api-key: <YOUR_API_KEY>'
```

### Update Cart

<hr>

```
curl --location --request PUT 'http://localhost/carts/<CART_ID>' \
--header 'x-api-key: <YOUR_API_KEY>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'customer_id=<YOUR_GENERATED_KEY>'
```

### Delete Cart

<hr>

```
curl --location --request DELETE 'http://localhost/carts/<CART_ID>' \
--header 'x-api-key: <YOUR_API_KEY>'
```

### Create Cart Item

<hr>

To create a cart item you need to is pass the following form fields:

-   cart_id
-   product_id
-   quantity
-   price

```
curl --location --request POST 'http://localhost/cartitems' \
--header 'x-api-key: <YOUR_API_KEY>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'cart_id=<YOUR_CART_ID>' \
--data-urlencode 'product_id=1' \
--data-urlencode 'quantity=1' \
--data-urlencode 'price=100'
```

### Update Cart Item

<hr>

Update a cart by passing in the followng field:

-   quantity

```
curl --location --request PUT 'http://localhost/cartsitems/<CART_ITEM_ID>' \
--header 'x-api-key: <YOUR_API_KEY>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'quantity=2'
```

### Delete Cart Item

<hr>

```
curl --location --request DELETE 'http://localhost/cartitems/<CART_ID>' \
--header 'x-api-key: <YOUR_API_KEY>'
```
