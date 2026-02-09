# Test Cases - TS-004: Validate Order Creation and Retrieval via Orders API (POST & GET)

These test cases validate the end-to-end behavior of the Orders API in a marketplace context, covering both order creation and order retrieval flows.

The goal of these test cases is to ensure that orders are correctly created, calculated, stored, protected, and retrieved according to business rules, security requirements, and API contract expectations.

---

## 🎯 Scope and Objectives

The TS-004 focuses on validating:

- Order creation using POST /orders
- Order retrieval using GET /orders/{orderId}
- Shipping fee rules per seller in a marketplace environment
- Data integrity between POST and GET operations
- Authentication and authorization constraints
- Proper error handling and HTTP status codes

---

## 🧩 Covered Cases

### POST /orders – Order Creation

The POST test cases validate:

- Successful order creation without shipping fee
- Successful order creation with shipping fee applied
- Validation errors when shipping fee rules are violated
- Handling of `null`, zero, or invalid shipping fee values
- Order creation with multiple sellers and multiple products
- Correct total price calculation per business rules
- Proper response structure and returned `orderId`

These tests ensure that all pricing and shipping rules are enforced by the system, not trusted from client input.

---

### GET /orders/{orderId} – Order Retrieval

The GET test cases validate:

- Successful retrieval of an order using a valid `orderId`
- Data consistency between the created order (POST) and retrieved order (GET)
- Behavior when requesting a non-existing or non-owned `orderId`
- Input validation for invalid `orderId` formats
- Authentication enforcement:
  - Missing token
  - Expired or invalid token
- Secure behavior preventing unauthorized access to order data

Special attention is given to security and data isolation, ensuring that users can retrieve only their own orders and that sensitive information is never exposed.

---

## 🔐 Security and Access Control Considerations

- Order access is protected by authentication tokens.
- Orders are user-scoped resources.
- When an order does not exist or does not belong to the authenticated user, the API returns 404 Not Found to avoid information disclosure.
- No separate authorization roles are assumed for order retrieval in this scenario.

---

## 🗂 Folder Structure
TS-004/

├── POST/

│ ├── TC-004.01 … TC-004.06

└── GET/

  └── TC-004.07 … TC-004.11


Each test case is documented individually, following a consistent structure with:

- Description  
- Preconditions  
- Endpoint and headers  
- Payload (when applicable)  
- Expected results  
- Business rules covered  

---

## ✅ Final Notes

These test cases demonstrates:

- Business-oriented test design
- Clear separation between creation and retrieval flows
- Strong focus on API contract validation
- Secure handling of edge cases
- Realistic marketplace behavior

