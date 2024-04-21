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

