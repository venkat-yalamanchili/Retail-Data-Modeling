# Data Dictionary

This data dictionary documents the final normalized OLTP schema for the retail sales order management project.

## customers

| Column | Data Type | Key | Required | Description |
|---|---|---|---|---|
| customer_id | BIGINT | PK | Yes | Surrogate identifier for a customer. |
| first_name | VARCHAR(100) |  | Yes | Customer first name. |
| last_name | VARCHAR(100) |  | Yes | Customer last name. |
| email | VARCHAR(255) | Unique | Yes | Customer email address. |
| phone_number | VARCHAR(30) |  | No | Customer phone number. |
| date_joined | DATE |  | Yes | Date the customer joined. |

## products

| Column | Data Type | Key | Required | Description |
|---|---|---|---|---|
| product_id | BIGINT | PK | Yes | Surrogate identifier for a product. |
| product_name | VARCHAR(200) |  | Yes | Product name. |
| category_id | BIGINT |  | Yes | Product category identifier. |
| price | NUMERIC(12,2) |  | Yes | Current product price. |
| stock_qty | INTEGER |  | Yes | Current available stock quantity. |

## store_branch

| Column | Data Type | Key | Required | Description |
|---|---|---|---|---|
| store_branch_id | BIGINT | PK | Yes | Surrogate identifier for a store branch. |
| store_branch_name | VARCHAR(150) | Unique | Yes | Store branch name. |
| store_branch_location | VARCHAR(255) |  | Yes | Store branch location. |

## orders

| Column | Data Type | Key | Required | Description |
|---|---|---|---|---|
| order_id | BIGINT | PK | Yes | Surrogate identifier for an order. |
| customer_id | BIGINT | FK | Yes | References the customer who placed the order. |
| order_date | TIMESTAMP |  | Yes | Date and time the order was placed. |
| total_amount | NUMERIC(12,2) |  | Yes | Total amount for the order. |
| store_branch_id | BIGINT | FK | Yes | References the branch that processed the order. |

## order_items

| Column | Data Type | Key | Required | Description |
|---|---|---|---|---|
| order_item_id | BIGINT | PK | Yes | Surrogate identifier for an order line. |
| order_id | BIGINT | FK | Yes | References the order header. |
| product_id | BIGINT | FK | Yes | References the product sold. |
| qty | INTEGER |  | Yes | Quantity sold on the order line. |
| line_amount | NUMERIC(12,2) |  | Yes | Sales amount for the order line. |

## payments

| Column | Data Type | Key | Required | Description |
|---|---|---|---|---|
| payment_id | BIGINT | PK | Yes | Surrogate identifier for a payment. |
| order_id | BIGINT | FK | Yes | References the order being paid. |
| payment_method | VARCHAR(50) |  | Yes | Method used for payment. |
| payment_amount | NUMERIC(12,2) |  | Yes | Amount paid. |
| payment_status | VARCHAR(30) |  | Yes | Payment processing status. |
| transaction_timestamp | TIMESTAMP |  | Yes | Payment transaction timestamp. |

## shipments

| Column | Data Type | Key | Required | Description |
|---|---|---|---|---|
| shipment_id | BIGINT | PK | Yes | Surrogate identifier for a shipment. |
| order_id | BIGINT | FK | Yes | References the shipped order. |
| shipping_carrier | VARCHAR(100) |  | Yes | Carrier used for delivery. |
| tracking_number | VARCHAR(100) | Unique | No | Carrier tracking number. |
| shipment_status | VARCHAR(30) |  | Yes | Shipment status. |
| estimated_delivery_date | DATE |  | No | Expected delivery date. |
