# Normalization Walkthrough

## Starting Point

The raw requirement analysis identified the following subjects:

- Customers
- Products
- Orders
- Store Branches
- Payments
- Shipments

The initial logical model placed order information, quantity, and branch details close to the order record. This was enough to understand the business process, but it was not fully normalized.

## Issue 1: Quantity on the Order Header

A single order can include many products. If quantity is stored only in the order header, the model cannot represent different quantities for different products.

### Change Made

Create `order_items` as a child table of `orders` and a bridge to `products`.

Before:

```text
orders(order_id, customer_id, order_date, total_amount, qty)
```

After:

```text
orders(order_id, customer_id, order_date, total_amount, store_branch_id)
order_items(order_item_id, order_id, product_id, qty, line_amount)
```

## Issue 2: Branch Details Repeated in Orders

Branch name and branch location describe the branch, not the order. If those values are repeated in every order, a branch name change would require many rows to be updated.

### Change Made

Create a separate `store_branch` master table and keep only `store_branch_id` in `orders`.

Before:

```text
orders(order_id, ..., store_branch_id, store_branch_name, store_branch_location)
```

After:

```text
store_branch(store_branch_id, store_branch_name, store_branch_location)
orders(order_id, ..., store_branch_id)
```

## Issue 3: Products Not Resolved into Orders

The product catalog exists separately, but sales analytics requires knowing which products were purchased in each order.

### Change Made

Use `order_items` to resolve the relationship between orders and products.

```text
orders 1 -> many order_items
products 1 -> many order_items
```

## Final Result

The final model is in third normal form for the stated requirements. It separates master data from transaction data, reduces redundancy, and supports multi-product orders, multiple payments, and multiple shipments.
