# Orders API - Documentation

## Overview
This documentation describes the structure, validation rules, and field definitions for the Orders API used in the marketplace scenario. It is used as a reference for API validation, test design, and defect analysis.

## Authentication
The API requires a valid authentication token. Requests without valid authentication must be rejected.

Requests must include:
`Authorization: Bearer <token>`

## Endpoint (example)
POST `/api/orders`
GET `/api/orders/{orderId}`

---
## Request Payload Structure

The request body must be a JSON object with the following structure:

### Root Object
| Field            | Type    | Required | Description                                                                 |
|------------------|---------|----------|-----------------------------------------------------------------------------|
| userId           | Integer | Yes      | Identifier of the user placing the order                                    |
| orderItems       | Array   | Yes      | List of products included in the order                                      |
| shippingBySeller | Array   | Yes      | Shipping configuration per seller                                           |
| totalPrice       | Decimal | No       | Optional client-provided value (must be validated by the system if present) |

---
### orderItems Object
Each entry represents one product in the order.

| Field     | Type    | Required | Description                                    |
|-----------|---------|----------|------------------------------------------------|
| productId | Integer | Yes      | Identifier of the product                      |
| quantity  | Integer | Yes      | Quantity purchased (must be > 0)               |
| unitPrice | Decimal | Yes      | Product unit price                             |
| sellerId  | Integer | Yes      | Identifier of the seller providing the product |

---
### shippingBySeller Object
Each entry represents shipping rules for one seller.

| Field                 | Type          | Required    | Description                                         |
|-----------------------|---------------|-------------|-----------------------------------------------------|
| sellerId              | Integer       | Yes         | Seller identifier (must match seller in orderItems) |
| hasShippingFee        | Boolean       | Yes         | Indicates whether shipping fee applies              |
| shippingFeeValue      | Decimal       | Conditional | Required only when `hasShippingFee = true`          |
| shippingType          | String (Enum) | Yes         | Delivery mode: `STANDARD` or `EXPRESS`              |
| estimatedDeliveryDays | Integer       | Yes         | Estimated delivery time in days                     |

---
## Validation Rules

### Data Integrity
- Each `sellerId` in `orderItems` must exist in `shippingBySeller`
- Each product must belong to the specified seller
- Quantities must be greater than zero

### Shipping Rules
- Shipping is calculated per seller, not per order
- `hasShippingFee` determines whether a shipping fee will be applied:
	- When `hasShippingFee = true`:
		- `shippingFeeValue` is mandatory.
		- `shippingFeeValue` must be greater than 0.00.
	- When `hasShippingFee = false`:
		- `shippingFeeValue` is not considered.
		- If provided, it must be ignored in the total price calculation.
- `shippingType` is mandatory for all sellers and must be a valid enum value.

### Total Price Calculation
The system must calculate the final total price.
Client-provided values must not be trusted without validation.

**Formula:**
```text
Total Price =
Sum of (quantity × unitPrice for all items)
+ Sum of shippingFeeValue for sellers where hasShippingFee = true
```
---
## Example Request
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

## Expected API Behavior
The API must:
- Validate authentication.
- Validate payload structure and required fields.
- Validate business rules.
- Calculate total price internally.
- Reject inconsistent data.
- Persist the order data reliably.
- Return a unique order identifier.
- Allow retrieval of stored orders.

## Usage in Testing
This document is used to:
- Design API test cases.
- Validate request structure and data types.
- Verify business logic enforcement.
- Support defect investigation.
- Ensure system-calculated totals are correct.


