# Test Cases – TS-004: Orders API (POST and GET)

This test suite validates the behavior of the Orders API in a marketplace context, covering order creation (POST) and order retrieval (GET), with test cases organized by HTTP method.

The focus is on business rules enforcement, price calculation, data consistency, authentication, and secure access to order data.

This module is supported by the following documentation available in this directory:

- [Orders API Documentation](orders-api-documentation.md) – Defines endpoints, request/response structures, and behavioral expectations.

- [Marketplace Database Documentation](marketplace-database-documentation.md) – Describes the relational model, entity responsibilities, and data validation rules.

Together, these documents provide the structural and functional context required to understand the test coverage defined in the TS-004.

At the end of this README, you will find direct links to each individual test case for easy navigation.

## Scope
The test cases of the TS-004 validates:

- Order creation and retrieval flows
- Seller-based shipping fee rules
- Order snapshot integrity at purchase time
- Price and total calculation accuracy
- Data consistency between POST and GET operations
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

## Test Cases
Click on a test case below to view its detailed specification.

### POST - Order Creation

- [TC-004.01 – Single seller, single product and no shipping fee](post/tc-004.01.md)

- [TC-004.02 – hasShippingFee = false and shipping fee value ignored](post/tc-004.02.md)

- [TC-004.03 – hasShippingFee = true and shipping fee value applied](post/tc-004.03.md)

- [TC-004.04 - hasShippingFee = true and shippingFeeValue = null](post/tc-004.04.md)

- [TC-004.05 - hasShippingFee = true and shippingFeeValue = 0](post/tc-004.05.md)

- [TC-004.06 - Multiple sellers and multiple products](post/tc-004.06.md)


### GET - Order Retrieval

- [TC-004.07 - Valid orderId](get/tc-004.07.md)

- [TC-004.08 - Non-existing orderId](get/tc-004.08.md)

- [TC-004.09 - Invalid orderId format](get/tc-004.09.md)

- [TC-004.10 - Missing authentication token](get/tc-004.10.md)

- [TC-004.11 - Expired or invalid token](get/tc-004.11.md)
