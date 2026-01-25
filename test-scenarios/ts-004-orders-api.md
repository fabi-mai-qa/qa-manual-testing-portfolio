# Test Scenario 004 – Validate Order Creation and Retrieval via Orders API (Marketplace with Shipping per Seller)

## ID: TS-004

**Description:**  
Verify that the Orders API correctly creates and retrieves purchase orders in a marketplace scenario, ensuring proper calculation of total price, correct handling of shipping rules per seller, data integrity, and enforcement of business and authorization rules.

**Preconditions:**  
- User account exists in the system.
- User is authenticated and has a valid API access token.
- Products exist in the system with valid IDs, prices and associated sellers.
- Sellers exist in the system with defined shipping rules.
- Orders API is available in the QA environment.
- API documentation (endpoints and expected payloads) is available.

**Scenario Flow:**  
- User authenticates and obtains a valid API token.
- User sends a request to create an order via the Orders API.
- Request contains:
	- One or more products.
	- Products associated with one or more sellers.
	- Shipping rules defined per seller.
- System validates:
	- Product data.
	- Seller associations.
	- Shipping fee rules per seller.
- System calculates:
	- Subtotal per seller.
	- Shipping fees per seller (when applicable).
	- Final total order price.
- System creates the order successfully.
- System returns the created order with a unique order ID.
- User retrieves the order details using the order ID.
- System returns the correct order data.
- System rejects invalid or unauthorized requests according to business rules.

**Expected Result:**  
- Orders are created only when request data is valid.
- Shipping fees are applied only for sellers where "hasShippingFee: true".
- Shipping type and delivery estimation are always considered per seller.
- The total order price is calculated correctly according to business rules.
- Invalid requests are rejected with appropriate error messages and HTTP status codes.
- Created orders can be retrieved correctly via API using a valid order ID.
- Unauthorized access is blocked according to security rules.

**Business Rules:**
- Each seller included in the order must have a valid shipping configuration.
- `hasShippingFee` determines whether a shipping fee will be applied:
	- When `hasShippingFee = true`:
		- `shippingFeeValue` is mandatory.
		- `shippingFeeValue` must be greater than 0.00.
	- When `hasShippingFee = false`:
		- `shippingFeeValue` is not considered.
		- If provided, it must be ignored in the total price calculation.
- `shippingType` is mandatory for all sellers.
- `estimatedDeliveryDays` is mandatory for all sellers.
- The final order total price is calculated as:
```text
Total Price =
Sum of (quantity × unitPrice for all items)
+ Sum of shippingFeeValue for sellers where hasShippingFee = true
```

**Example Request Payload:**
```json
{
  "userId": 123,
  "orderItems": [
    {
      "productId": 10,
      "quantity": 2,
      "unitPrice": 50.00,
      "sellerId": 145
    },
    {
      "productId": 22,
      "quantity": 1,
      "unitPrice": 30.00,
      "sellerId": 200
    }
  ],
  "shippingBySeller": [
    {
      "sellerId": 145,
      "hasShippingFee": false,
      "shippingType": "STANDARD",
      "estimatedDeliveryDays": 7
    },
    {
      "sellerId": 200,
      "hasShippingFee": true,
      "shippingFeeValue": 15.00,
      "shippingType": "EXPRESS",
      "estimatedDeliveryDays": 3
    }
  ],
  "totalPrice": 145.00
}
``` 
