# Marketplace Database - Documentation

## Overview
This document describes the database structure required to support validation of the Orders API in the marketplace scenario.

It focuses on the tables, relationships, and fields that must be verified to ensure correct data persistence, integrity, and business rule enforcement after API operations.

This documentation supports SQL validation queries used during API integration testing.

For consistency, the SQL examples and queries in this document follow the syntax of Microsoft SQL Server, which may differ slightly from other database systems such as Oracle or MySQL.

## Scope
The following entities are required in the database for the scope validation of Orders API integration testing:

- `user`
- `seller`
- `shipping_type`
- `product_type`
- `product`
- `seller_product`
- `order`
- `order_status`
- `order_item`
- `order_shipping`
---

# user
Stores registered users who can create purchase orders.

This table is validated indirectly through Orders API integration tests to ensure correct user-order relationship and referential integrity.

| Column        | Type         | PK  | FK | Required | Description                          |
| ------------- | ------------ | --- | -- | -------- | ------------------------------------ |
| user_id        | INT          | Yes | No | Yes      | Unique user identifier               |
| user_name      | VARCHAR(80)  | No  | No | Yes      | User name                            |
| user_email     | VARCHAR(255) | No  | No | Yes      | Unique email used for authentication |
| user_created_at | DATETIME     | No  | No | Yes      | Record creation timestamp            |
---

# seller
Stores registered marketplace sellers who offer products in the platform.

Shipping configuration is defined at `seller_product` level and validated through relationships during Orders API integration testing.

This table is validated through its relationships with `seller_product`, `order_item`, and `order_shipping` to ensure referential integrity.

| Column          | Type         | PK  | FK | Required | Description              |
| --------------- | ------------ | --- | -- | -------- | ------------------------ |
| seller_id        | INT          | Yes | No | Yes      | Unique seller identifier |
| seller_name      | VARCHAR(80)  | No  | No | Yes      | Seller name              |
| seller_email     | VARCHAR(255) | No  | No | Yes      | Seller email used for authentication       |
| seller_created_at | DATETIME     | No  | No | Yes      | Record creation timestamp     |
---

# shipping_type
Stores system-defined shipping types available for `seller_product` configuration.

This table acts as a reference catalog and is linked to `seller_product` and `order_shipping` to ensure consistency and historical traceability during Orders API integration testing.

| Column                 | Type          | PK  | FK | Required | Description                            |
|------------------------|---------------|-----|----|----------|--------------------------------------- |
| shipping_type_id         | INT           | Yes | No | Yes      | Unique shipping type identifier        |
| shipping_type_name       | VARCHAR(255)  | No  | No | Yes      | Unique shipping type display name      |
| has_shipping_fee	 | CHAR(1)	 | No  | No | Yes      | Indicates if the default seller_product_shipping_fee_value defined by the seller will be applied. Allowed values: 'Y'(uses shipping fee) , 'N'(does not use shipping fee)|
---

# product_type
Stores system-defined product categories used to classify marketplace products.

This table acts as a reference catalog and is validated indirectly through its relationship with `product` during Orders API integration testing.

| Column                | Type          | PK  | FK | Required | Description                      |
|-----------------------|---------------|-----|----|----------|----------------------------------|
| product_type_id         | INT           | Yes | No | Yes      | Unique product type identifier   |
| product_type_name       | VARCHAR(255)  | No  | No | Yes      | Unique product type display name |
| product_type_created_at  | DATETIME      | No  | No | Yes      | Record creation timestamp        |
---

# product
Stores marketplace catalog products independently of sellers, pricing, or shipping configuration.

Products are classified by `product_type` and become sellable only when associated with a seller in `seller_product`.

This table is referenced during order creation through Seller Products and validated via referential integrity checks in Orders API integration testing.

| Column            | Type          | PK | FK | Required | Description                 |
|-------------------|---------------|----|----|----------|-----------------------------|
| product_id         | INT           | Yes| No | Yes      | Unique product identifier   |
| product_name       | VARCHAR(255)  | No | No | Yes      | Product display name        |
| product_type_id     | INT           | No | Yes| Yes      | Product type classification |
| product_created_at  | DATETIME      | No | No | Yes      | Record creation timestamp   |
---

# seller_product
Stores seller-specific commercial offerings derived from marketplace catalog products.

This table defines pricing, shipping configuration, and availability rules for each seller-product combination. It is directly validated during Orders API integration testing, particularly for shipping fee rules applied per seller.

The `seller_product` table represents the primary business validation layer before order persistence.

| Column                       | Type          | PK | FK | Required | Description                                          |
|------------------------------|---------------|----|----|----------|----------------------------------------------------- |
| seller_product_id              | INT           | Yes| No | Yes      | Unique seller-product offer identifier               |
| seller_id                     | INT           | No | Yes| Yes      | Seller offering this product 		           |
| product_id                    | INT           | No | Yes| Yes      | Reference to the associated catalog product          |
| seller_product_unit_price       | NUMERIC(10,2) | No | No | Yes      | Selling price defined by the seller for this offer |
| seller_product_active          | CHAR(1)       | No | No | Yes      | Indicates if the product is active for sale. Allowed values: 'Y' (active), 'N' (inactive)|
| seller_product_shipping_type_id  | INT           | No | Yes| Yes      | Reference to the default shipping method configured by the seller|
| seller_product_shipping_fee_value| NUMERIC(10,2) | No | No | Yes      | Default shipping fee defined by the seller|
---

# order
Stores persisted purchase orders created by buyers in the marketplace. 

This table represents the immutable financial and transactional snapshot of the order at the moment of checkout, ensuring data integrity, auditability, and historical traceability.
At the time of order creation, `order_created_at` and `order_updated_at` store the same timestamp. After creation, only `order_updated_at` is modified when the order status changes.

The Orders table acts as the transactional aggregation layer, consolidating item-level and seller-level shipping calculation into a finalized purchase record.

| Column                   | Type          | PK  | FK  | Required | Description |
|---------------------------|--------------|-----|-----|----------|-------------|
| order_id                  | INT           | Yes | No  | Yes      | Unique order identifier |
| user_id                   | INT           | No  | Yes | Yes      | Buyer who placed the order |
| order_status_id            | INT           | No  | Yes | Yes      | Reference to the current order status |
| order_created_at           | TIMESTAMP     | No  | No  | Yes      | Timestamp when the order was created |
| order_updated_at           | TIMESTAMP     | No  | No  | Yes      | Timestamp of the most recent order status update |
| order_total_items_amount    | NUMERIC(10,2) | No  | No  | Yes      | Aggregated subtotal of all order items at purchase time |
| order_total_shipping_amount | NUMERIC(10,2) | No  | No  | Yes      | Aggregated shipping fees applied per seller at purchase time |
| order_total_amount         | NUMERIC(10,2) | No  | No  | Yes      | Final total amount charged to the buyer (items + shipping) |
---

# order_status
Stores system-defined order status values used to represent the current lifecycle stage of an order.

This table serves as a reference catalog associated with `order`. It is structural (non-transactional) and does not store status history.

| Column                   | Type          | PK  | FK  | Required | Description                     |
| ------------------------ | ------------- | --- | --- | -------- | ------------------------------- |
| order_status_id            | INT           | Yes | No  | Yes      | Unique order status identifier  |
| order_status_name          | VARCHAR(80)   | No  | No  | Yes      | Unique display status name 	    |
---

# order_item
Stores the items of an order, linking each item to a specific seller offer.

This table represents the financial snapshot of each item at the time of purchase, preserving seller, price, and quantity data independently from future catalog changes.

| Column                 | Type          | PK  | FK  | Required | Description    					 |
| ---------------------- | ------------- | --- | --- | ---------|--------------------------------------------------------|
| order_item_id            | INT           | Yes | No  | Yes      | Unique order line item identifier	        	 |
| order_id                | INT           | No  | Yes | Yes      | References the associated order       		 |
| seller_id               | INT           | No  | Yes | Yes      | Seller identifier at purchase time                     |
| seller_product_id        | INT           | No  | Yes | Yes      | Seller-product offer selected at the time of purchase  |
| seller_product_unit_price | NUMERIC(10,2) | No  | No  | Yes      | Unit price applied at purchase time 			 |
| order_item_quantity      | INT           | No  | No  | Yes      | Quantity purchased 			 		 |
| order_item_subTotal      | NUMERIC(10,2) | No  | No  | Yes      | Calculated subtotal for this item at purchase time|
---

# order_shipping
Stores the shipping details applied to an order at purchase time.
This table preserves the shipping type, fee, and delivery estimation associated with each seller offer, ensuring consistency even if seller configurations change later.

| Column                | Type          | PK | FK | Required | Description |
|-----------------------|---------------|----|----|----------|-------------|
| order_shipping_id       | INT           | Yes| No | Yes      | Unique shipping record identifier 	  	  	  |
| order_id               | INT           | No | Yes| Yes      | References the associated order 		  	  	  |
| seller_product_id       | INT           | No | Yes| Yes      | Seller-product offer linked to this shipping record	  |
| has_shipping_fee        | CHAR(1)       | No | No | Yes      | Indicates whether a shipping fee was applied (Y/N) 	  |
| seller_product_shipping_fee_value | NUMERIC(10,2) | No | No | Yes      | Shipping fee applied at purchase time		  	  |
| seller_product_shipping_type_id | INT           | No | Yes| Yes      | Shipping type used for this seller-product at purchase time|
| estimated_delivery_days | INT           | No | No | Yes      | Delivery estimation at purchase time 	 	  	  |
---

# Data Validation Rules
The database must enforce the following rules and structural principles:

## 1.Referential Integrity
- Orders must reference a valid `user_id`.
- Order Items must reference active and active `seller_product_id` at the purchase moment.
- Order shipping records must reference a valid `seller_product_id` and it must match the `seller_product_id` in the Order Items.
- All foreign keys must enforce relational consistency.

## 2.Seller Product Governance
- The Seller Products Table is the central commercial configuration entity.
- It defines:
	- Which products a seller currently offers (Active status).
	- Which products were previously sold by the seller before (Inactive status).
	- The system-defined `shipping_type_id` used by the seller.
	- Whether the `shipping_type_id` applies the shipping fee (defined by `has_shipping_fee`) .
	- The default `shipping_fee_value`.
- Only active seller products can be purchased.

## 3.System-Defined Tables
- The following tables are system-defined and managed exclusively by the system:
	- `shipping_type`
	- `product_type`
	- `order_status`
- Their records cannot be modified directly by sellers.

## 4.Order Snapshot and Historical Integrity
- The following tables store a snapshot of data at the purchase moment:
	- `order`
	- `order_item`
	- `order_shipping`
- These tables must:
	- Persist the unit price applied at purchase time.
	- Persist the shipping type used.
	- Persist the shipping fee applied.
	- Persist the calculated subtotal and total values.
	- Remain immutable after checkout completion.
- Post-checkout updates must not alter historical commercial data.

## 5.Order Integrity Constraints
- Each order must contain at least one order item.
- Stored order totals must match the system-calculated totals.
- Order item subtotal must equal:
	`seller_product_unit_price x order_item_quantity`
- Order total must equal:
	**Sum of order items + Sum of shipping fees**



