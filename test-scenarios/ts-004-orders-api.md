## Test Scenario 004 - Validate Order Creation and Retrieval via Orders API (Marketplace with Shipping per Seller)

### ID: TS-004

**Description:**  
Verify that the Orders API correctly creates and retrieves purchase orders in a marketplace scenario, ensuring accurate total calculation, proper handling of shipping rules per seller, data integrity, and enforcement of business and authorization rules.

**Preconditions:**  
- User is authenticated and has a valid API access token.
- Products exist in the system with valid IDs, prices and associated sellers.
- Sellers exist and have defined shipping rules.
- Orders API is available in the QA environment.
- API documentation is available.

**Scenario Flow:**  
- User authenticates and obtains a valid API token.
- User sends a request to create an order containing products from one or more sellers.
- System validates request structure, product data, seller associations, and shipping fee rules per seller.
- System calculates item subtotals, shipping fees per seller (when applicable) and the final total order price.
- System creates the order and returns a unique order ID.
- User retrieves the order using the returned ID.
- System returns consistent order data.
- System rejects invalid or unauthorized requests according to business rules.

**Expected Result:**  
- Orders are created only when request data is valid.
- Shipping fees are applied only for sellers where "hasShippingFee: true".
- Shipping type and delivery estimation are validated and applied per seller.
- Total order price is calculated accurately by the system.
- Created and stored orders can be retrieved with consistent values via API using a valid order ID.
- Invalid or unauthorized requests are rejected with appropriate error messages and HTTP status codes according to validation and security rules.

**Business Rules:**
- Each order item must reference a valid product and seller.
- Shipping rules are applied per seller, not per order.
- Mandatory fields and data types must be validated.
- Order totals must be calculated by the system, not trusted from the request.
- Unauthorized requests must be rejected.

## Payload information:
To check details about the API Documentation, click the link below:
- [Orders API - Documentation](../test-cases/test-cases-ts-004-orders-api/orders-api-documentation.md)

## Database information:
To check details about the database table structure and data validation, click the link below:
- [Marketplace database and data validation](../test-cases/test-cases-ts-004-orders-api/marketplace-database-documentation.md)

