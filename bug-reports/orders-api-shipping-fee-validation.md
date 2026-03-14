# Orders API incorrectly applies shipping fee when shipping type does not require it

## Bug Description
The Orders API is applying a shipping fee even when the associated shipping type indicates that no shipping fee should be applied (`has_shipping_fee = N`).
During the order creation, the payload correctly specifies that the seller does not apply shipping fees. The database configuration also indicates that the selected shipping type does not require a shipping fee.
However, the system persists a shipping fee value and includes it in the order total calculation.

► ***To better understand this bug report, it is recommended to review the following supporting documentation first:***
  - [API Documentation (Order API)](test-cases/test-cases-ts-004-orders-api/orders-api-documentation.md)
  - [Database Documentation (Marketplace DB)](test-cases/test-cases-ts-004-orders-api/marketplace-database-documentation.md)

---

## Environment
**Service:** Orders API

**Endpoint:** POST /orders

**Database:** Relational SQL Server database

---

## Order Creation Flow
```text
Client Request
      ↓
Orders API
      ↓
Shipping Fee Validation ← ⚠ Bug occurs here
      ↓
Order Persistence
      ↓
Order Total Calculation 
```

---

## Steps to Reproduce
1. Ensure that a seller product exists with the following configuration:
   - seller_product_shipping_type_id = 2
   - seller_product_shipping_fee_value > 0

2. Ensure that another seller product exists with:
   - seller_product_shipping_type_id = 1
   - seller_product_shipping_fee_value > 0

3. Send a POST request to `/orders` with:
   - seller 145 → hasShippingFee = false
   - seller 200 → hasShippingFee = true
		→ shippingFeeValue = 15 (example)

4. Create the order.

5. Retrieve the order data from the database.

6. Compare the expected shipping total with the persisted value.

---

## Request Payload
```json
{
  "userId": 123,
  "orderItems": [
    {
      "productId": 11,
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
  ]
}
```

## API Response
```json
{
  "orderId": 179
}
```

---

## Database Evidence and Investigation Queries
Queries used to investigate the root cause of this issue:

### First query - The Detection Query:
With this query we are able to detect a discrepancy between the expected shipping total and the persisted value.
```sql
SELECT o.order_id,
       o.order_total_items_amount,
       o.order_total_shipping_amount,
       o.order_total_amount,
       oi.items_total,
       os.shipping_total
  FROM [order] o
  JOIN (
	  SELECT order_id,
	     SUM (order_item_subtotal) AS items_total
	    FROM order_item
	   GROUP BY order_id
	) oi
    ON oi.order_id = o.order_id
  JOIN (
	  SELECT order_id,
	     SUM (shipping_fee_value) AS shipping_total
	    FROM order_shipping
	   WHERE has_shipping_fee = 'Y'
	   GROUP BY order_id
	) os
    ON os.order_id = o.order_id
 WHERE o.order_id = 179;
```
### Expected result from the query above:
| order_id | order_total_items_amount | order_total_shipping_amount | order_total_amount | items_total | shipping_total |
|----------|--------------------------|-----------------------------|--------------------|-------------|----------------|
| 179 	   | 130.00  	              | 25.00			    | 155.00 		 | 130.00      | 15.00          |
--- 

### Second query - The Root Cause Query:
With this query we are able to diagnose where specifically this additional data is coming from.
```sql
SELECT os.order_id,
       os.seller_product_id,
       os.shipping_type_id,
       os.has_shipping_fee AS has_shipping_fee_os,
       os.shipping_fee_value,
       st.shipping_type_name,
       st.has_shipping_fee AS has_shipping_fee_st
FROM order_shipping os
JOIN shipping_type st
  ON st.shipping_type_id = os.shipping_type_id
WHERE os.order_id = 179;
```
### Expected result from the query above:
| order_id | seller_product_id | shipping_type_id | has_shipping_fee_os | shipping_fee_value | shipping_type_name    | has_shipping_fee_st |
|----------|-------------------|------------------|---------------------|--------------------|------------------------|---------------------|
| 179 	   | 11  	       | 2		  | N 		  	| 10.00              | Does Not Apply Shipping Fee | N		    |
| 179 	   | 22  	       | 1		  | Y 		 	| 15.00 	     | Applies Shipping Fee   | Y 		    |
---

### Third query - The Business Rule Query:
With this query we are able to validate the fixed business rule registered in the database table `shipping_type` where `shipping_type_id` is the primary key used to link the business rule to the seller and product as a foreign key.
```sql
SELECT *
  FROM shipping_type;
```
### Expected result from the query above:
| shipping_type_id | shipping_type_name         | has_shipping_fee |
|------------------|----------------------------|------------------|
| 1		   | Applies Shipping Fee       | Y 		   |
| 2	    	   | Does Not Apply Shipping Fee| N		   |
---

## Expected Result
Shipping fees should only be applied when the shipping type requires it. 
Even if the `seller_product_shipping_fee_value` is greater than zero in the database, the system should ignore this value when the shipping type does not require a shipping fee.

### Expected Calculation:
```text
Items total = 130
Shipping total = 15
Order total = 145
``` 
---

## Actual Result
The order persisted the following totals (summarized view):
```text
Items total = 130
Shipping total = 25
Order total = 155
```
This indicates that an additional shipping fee of 10.00 was applied incorrectly.

Below is the persisted order related data in database (detailed view):
# order
| order_id | user_id | order_status_id | order_created_at | order_updated_at | order_total_items_amount | order_total_shipping_amount | order_total_amount |
|----------|---------|-----------------|------------------|------------------|--------------------------|-----------------------------|--------------------|
| 179 	   | 123     | 1  	       | 2026-03-05 07:30:45 | 2026-03-05 07:30:45 | 130.00	        | 25.00			      | 155.00 		   |

# order_item
| order_item_id | order_id | seller_id | seller_product_id | seller_product_unit_price | order_item_quantity | order_item_subtotal |
|---------------|----------|-----------|-------------------|---------------------------|---------------------|---------------------|
| 214 	   	| 179      | 145       | 11		   | 50.00		       | 2   	             | 100.00		   |
| 215 	   	| 179      | 200       | 22		   | 30.00		       | 1   	             |  30.00		   |

# order_shipping
| order_shipping_id | order_id | seller_product_id | has_shipping_fee | shipping_fee_value | shipping_type_id | estimated_delivery_days |
|-------------------|----------|-------------------|------------------|--------------------|------------------|-------------------------|
| 198 		    |179       | 11     	   | N  	      | 10.00		   | 2	 	      | 7		        |
| 199 		    |179       | 22     	   | Y  	      | 15.00		   | 1	 	      | 3		        |

---

## Root Cause Hypothesis
The Orders service appears to be applying the shipping fee value without validating the rule defined in the `shipping_type` table.

As a result, a shipping fee is being incorrectly added in the order total calculation.

---

## Impact
Incorrect financial calculation in the order totals.

Possible impacts:
- Incorrect order totals
- Billing inconsistencies
- Loss of system reliability
- Financial reporting inaccuracies

## Severity
**High**

Reason:
This bug affects financial calculations during the order processing.
