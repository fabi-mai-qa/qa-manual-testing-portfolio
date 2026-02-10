# Test Cases – TS-004: Orders API (POST and GET)

This test suite validates the behavior of the Orders API in a marketplace context, covering order creation (POST) and order retrieval (GET), with test cases organized by HTTP method.

The focus is on business rules enforcement, price calculation, data consistency, authentication, and secure access to order data.

## Scope
The test cases of the TS-004 validates:

- Order creation and retrieval flows
- Shipping fee rules per seller
- Data integrity between POST and GET
- Authentication and error handling
- Proper HTTP status codes

## Covered Cases

### POST /orders
- Order creation with and without shipping fee
- Validation of invalid or missing shipping fee values
- Orders with multiple sellers and products
- Correct total price calculation
- Proper response structure and returned `orderId`

### GET /orders/{orderId}
- Successful order retrieval using a valid `orderId`
- Data consistency between POST and GET
- Non-existing or non-owned order handling
- Invalid `orderId` format validation
- Authentication scenarios (expired, or invalid token)

These test cases ensure secure access, correct business behavior, and compliance with the Orders API contract.



