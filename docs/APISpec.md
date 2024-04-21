# API Specification for CSC Project 

## 1. Customer Purchasing

The API calls are made in this sequence when making a purchase:
1. `Get Listings`
2. `Create Cart`
3. `Add Item to Cart` (Can be called multiple times)
4. `Checkout Cart`

### 1.1. Get Listings - `/listings` (GET)

Retrieves the list of available shoe listings based on optional filters like size, brand, and price.

**Query Parameters**:
- `size` (optional): Shoe size to filter by.
- `brand` (optional): Brand name to filter by.
- `max_price` (optional): Maximum price to filter by.

**Response**:

```json
[
    {
        "listing_id": "integer",
        "title": "string",
        "brand": "string",
        "size": "integer",
        "price": "integer",
        "images": ["string"]
    }
]
```

### 1.2. Create Cart - `/carts` (POST)

Creates a new shopping cart for the customer.

**Response**:

```json
{
    "cart_id": "string" /* This ID will be used for future calls to add items and checkout */
}
```

### 1.3. Add Item to Cart - `/carts/{cart_id}/items/{listing_id}` (PUT)

Adds a specific shoe listing to the customer's cart or updates the quantity of an existing item in the cart.

**Request**:

```json
{
  "quantity": "integer"
}
```

**Response**:

```json
{
    "success": "boolean"
}
```

### 1.4. Checkout Cart - `/carts/{cart_id}/checkout` (POST)

Processes the checkout of the cart, including payment handling and order confirmation.

**Request**:

```json
{
  "payment_method": "string",
  "shipping_address": "string"
}
```

**Response**:

```json
{
    "total_items": "integer",
    "total_amount": "integer"
}
```

## Example Flows

### Example Flow 1: New User Registration and First Purchase

1. User registers by sending their details to `POST /users`.
2. User logs in via `POST /auth/login` and receives a token.
3. User browses shoes by calling `GET /listings` with filters applied.
4. User creates a cart via `POST /carts`.
5. User adds shoes to the cart by calling `PUT /carts/{cart_id}/items/{listing_id}` multiple times.
6. User checks out by calling `POST /carts/{cart_id}/checkout`.

### Example Flow 2: Repeat Customer Purchase

1. Returning user logs in via `POST /auth/login` to retrieve their session token.
2. User retrieves the latest shoe listings via `GET /listings`.
3. User reuses an existing cart or creates a new one via `POST /carts`.
4. User adds multiple shoes to their cart.
5. Completes the purchase with `POST /carts/{cart_id}/checkout`.

### Example Flow 3: Admin Adding New Listings

1. Admin logs in to obtain a session token.
2. Admin posts new shoe listings via `POST /listings`.
3. Admin views all listings to verify new entries via `GET /listings`.
