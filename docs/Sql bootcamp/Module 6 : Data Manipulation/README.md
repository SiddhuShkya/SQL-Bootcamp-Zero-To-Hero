## Module 6: Data Manipulation

### INSERT - Adding Data

```sql
-- Insert single row
INSERT INTO customers (first_name, last_name, email)
VALUES ('Alice', 'Johnson', 'alice@email.com');

-- Insert multiple rows
INSERT INTO products (product_name, price, category_id)
VALUES 
    ('Laptop Pro', 1299.99, 1),
    ('Wireless Mouse', 29.99, 2),
    ('USB Cable', 9.99, 2);

-- Insert from SELECT
INSERT INTO archived_orders (order_id, customer_id, order_date)
SELECT id, customer_id, order_date
FROM orders
WHERE order_date < '2023-01-01';
```

### UPDATE - Modifying Data

```sql
-- Update single row
UPDATE products
SET price = 39.99
WHERE id = 5;

-- Update multiple columns
UPDATE customers
SET 
    email = 'newemail@example.com',
    phone = '555-1234'
WHERE id = 10;

-- Update with calculation
UPDATE products
SET price = price * 1.10
WHERE category_id = 3;

-- Update based on another table
UPDATE products
SET stock_quantity = stock_quantity - order_items.quantity
FROM order_items
WHERE products.id = order_items.product_id
  AND order_items.order_id = 100;
```

### DELETE - Removing Data

```sql
-- Delete specific rows
DELETE FROM customers
WHERE id = 15;

-- Delete with condition
DELETE FROM orders
WHERE status = 'cancelled'
  AND order_date < '2023-01-01';

-- Delete all rows (careful!)
DELETE FROM temp_table;

-- Better for deleting all: TRUNCATE (faster, resets auto-increment)
TRUNCATE TABLE temp_table;
```

### Transactions - ACID Properties

Transactions ensure data integrity.

```sql
-- Start transaction
BEGIN TRANSACTION;

-- Perform operations
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

-- If everything is okay
COMMIT;

-- If there's an error
ROLLBACK;
```

**Example with error handling:**
```sql
BEGIN TRANSACTION;

UPDATE products SET stock_quantity = stock_quantity - 5 WHERE id = 10;

-- Check if product had enough stock
IF (SELECT stock_quantity FROM products WHERE id = 10) < 0 THEN
    ROLLBACK;
ELSE
    INSERT INTO order_items (order_id, product_id, quantity) 
    VALUES (100, 10, 5);
    COMMIT;
END IF;
```