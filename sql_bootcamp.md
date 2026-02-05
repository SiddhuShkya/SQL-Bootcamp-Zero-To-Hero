# SQL Bootcamp: Zero to Hero

A comprehensive guide to mastering SQL from absolute beginner to advanced practitioner.

---

## Table of Contents

1. [Introduction & Setup](#introduction--setup)
2. [Module 1: SQL Fundamentals](#module-1-sql-fundamentals)
3. [Module 2: Filtering & Sorting](#module-2-filtering--sorting)
4. [Module 3: Aggregate Functions](#module-3-aggregate-functions)
5. [Module 4: Joins](#module-4-joins)
6. [Module 5: Subqueries](#module-5-subqueries)
7. [Module 6: Data Manipulation](#module-6-data-manipulation)
8. [Module 7: Advanced Queries](#module-7-advanced-queries)
9. [Module 8: Database Design](#module-8-database-design)
10. [Module 9: Performance Optimization](#module-9-performance-optimization)
11. [Module 10: Real-World Projects](#module-10-real-world-projects)

---

## Introduction & Setup

### What is SQL?

SQL (Structured Query Language) is the standard language for managing and manipulating relational databases. It's used by data analysts, developers, and database administrators worldwide.

### Getting Started

**Recommended Tools:**
- SQLite (lightweight, no installation needed)
- MySQL Workbench (for MySQL)
- PostgreSQL + pgAdmin
- Online: SQLFiddle, DB Fiddle, or SQLiteOnline

**Sample Database:**
Throughout this bootcamp, we'll use an e-commerce database with the following tables:
- `customers` - customer information
- `products` - product catalog
- `orders` - order records
- `order_items` - individual items in orders
- `categories` - product categories

---

## Module 1: SQL Fundamentals

### Understanding Databases

A database is an organized collection of data. Tables are the foundation:

```
Table: customers
+----+------------+-----------+------------------+
| id | first_name | last_name | email            |
+----+------------+-----------+------------------+
| 1  | John       | Doe       | john@email.com   |
| 2  | Jane       | Smith     | jane@email.com   |
+----+------------+-----------+------------------+
```

### SELECT Statement - Your First Query

The `SELECT` statement retrieves data from a database.

**Basic Syntax:**
```sql
SELECT column1, column2
FROM table_name;
```

**Examples:**

```sql
-- Select all columns
SELECT * FROM customers;

-- Select specific columns
SELECT first_name, email FROM customers;

-- Select with alias (renaming columns)
SELECT 
    first_name AS "First Name",
    last_name AS "Last Name"
FROM customers;
```

### DISTINCT - Removing Duplicates

```sql
-- Get unique cities
SELECT DISTINCT city FROM customers;

-- Get unique combinations
SELECT DISTINCT city, state FROM customers;
```

### Practice Exercises - Module 1

1. Retrieve all product names and prices
2. Get a list of all unique categories
3. Select customer first names with an alias "Customer Name"

---

## Module 2: Filtering & Sorting

### WHERE Clause - Filtering Data

The `WHERE` clause filters records based on conditions.

```sql
-- Equal to
SELECT * FROM products WHERE price = 29.99;

-- Not equal to
SELECT * FROM products WHERE category_id != 1;

-- Comparison operators
SELECT * FROM products WHERE price > 50;
SELECT * FROM products WHERE stock_quantity <= 10;

-- Multiple conditions with AND
SELECT * FROM products 
WHERE price > 20 AND category_id = 3;

-- Multiple conditions with OR
SELECT * FROM products 
WHERE category_id = 1 OR category_id = 2;

-- Combining AND and OR (use parentheses!)
SELECT * FROM products 
WHERE (category_id = 1 OR category_id = 2) 
  AND price < 100;
```

### IN Operator

```sql
-- Instead of multiple OR conditions
SELECT * FROM products 
WHERE category_id IN (1, 2, 3);

-- Exclude multiple values
SELECT * FROM products 
WHERE category_id NOT IN (1, 2, 3);
```

### BETWEEN Operator

```sql
-- Price range
SELECT * FROM products 
WHERE price BETWEEN 20 AND 50;

-- Date range
SELECT * FROM orders 
WHERE order_date BETWEEN '2024-01-01' AND '2024-12-31';
```

### LIKE Operator - Pattern Matching

```sql
-- Starts with 'A'
SELECT * FROM customers 
WHERE first_name LIKE 'A%';

-- Ends with 'son'
SELECT * FROM customers 
WHERE last_name LIKE '%son';

-- Contains 'tech'
SELECT * FROM products 
WHERE product_name LIKE '%tech%';

-- Second letter is 'a'
SELECT * FROM customers 
WHERE first_name LIKE '_a%';

-- Case-insensitive in most databases
SELECT * FROM products 
WHERE product_name LIKE '%laptop%';
```

### IS NULL / IS NOT NULL

```sql
-- Find customers without phone numbers
SELECT * FROM customers 
WHERE phone IS NULL;

-- Find customers with email addresses
SELECT * FROM customers 
WHERE email IS NOT NULL;
```

### ORDER BY - Sorting Results

```sql
-- Sort ascending (default)
SELECT * FROM products 
ORDER BY price;

-- Sort descending
SELECT * FROM products 
ORDER BY price DESC;

-- Multiple columns
SELECT * FROM customers 
ORDER BY last_name, first_name;

-- Order by column position
SELECT product_name, price 
FROM products 
ORDER BY 2 DESC;  -- Orders by price (2nd column)
```

### LIMIT - Restricting Results

```sql
-- Get top 10 most expensive products
SELECT * FROM products 
ORDER BY price DESC 
LIMIT 10;

-- Pagination (MySQL/PostgreSQL)
SELECT * FROM products 
LIMIT 20 OFFSET 40;  -- Skip 40, get next 20

-- SQL Server uses TOP
SELECT TOP 10 * FROM products 
ORDER BY price DESC;
```

### Practice Exercises - Module 2

1. Find all products priced between $10 and $50
2. Get customers whose last names start with 'M'
3. Find the 5 cheapest products
4. List all orders from January 2024, sorted by date
5. Find products that are out of stock (quantity = 0)

---

## Module 3: Aggregate Functions

### COUNT - Counting Rows

```sql
-- Count all rows
SELECT COUNT(*) FROM customers;

-- Count non-null values
SELECT COUNT(phone) FROM customers;

-- Count distinct values
SELECT COUNT(DISTINCT city) FROM customers;
```

### SUM - Adding Values

```sql
-- Total revenue
SELECT SUM(total_amount) FROM orders;

-- Total quantity ordered
SELECT SUM(quantity) FROM order_items;
```

### AVG - Average Values

```sql
-- Average product price
SELECT AVG(price) FROM products;

-- Average order value
SELECT AVG(total_amount) FROM orders;
```

### MIN and MAX

```sql
-- Cheapest and most expensive products
SELECT 
    MIN(price) AS cheapest,
    MAX(price) AS most_expensive
FROM products;
```

### GROUP BY - Grouping Data

Group rows that have the same values and apply aggregate functions.

```sql
-- Count customers per city
SELECT 
    city, 
    COUNT(*) AS customer_count
FROM customers
GROUP BY city;

-- Total sales per product
SELECT 
    product_id,
    SUM(quantity) AS total_sold,
    SUM(quantity * unit_price) AS revenue
FROM order_items
GROUP BY product_id;

-- Multiple grouping columns
SELECT 
    city,
    state,
    COUNT(*) AS customer_count
FROM customers
GROUP BY city, state
ORDER BY customer_count DESC;
```

### HAVING - Filtering Grouped Data

`WHERE` filters before grouping, `HAVING` filters after grouping.

```sql
-- Cities with more than 10 customers
SELECT 
    city,
    COUNT(*) AS customer_count
FROM customers
GROUP BY city
HAVING COUNT(*) > 10;

-- Products with total sales over $1000
SELECT 
    product_id,
    SUM(quantity * unit_price) AS revenue
FROM order_items
GROUP BY product_id
HAVING SUM(quantity * unit_price) > 1000
ORDER BY revenue DESC;

-- Combining WHERE and HAVING
SELECT 
    category_id,
    AVG(price) AS avg_price
FROM products
WHERE price > 10  -- Filter before grouping
GROUP BY category_id
HAVING AVG(price) < 100  -- Filter after grouping
ORDER BY avg_price DESC;
```

### Practice Exercises - Module 3

1. Calculate total revenue from all orders
2. Find the average price per product category
3. Count how many orders each customer has placed
4. Find categories with more than 50 products
5. Get the total quantity sold for each product, but only for products that sold more than 100 units

---

## Module 4: Joins

Joins combine rows from two or more tables based on related columns.

### INNER JOIN

Returns only matching rows from both tables.

```sql
-- Join customers with their orders
SELECT 
    customers.first_name,
    customers.last_name,
    orders.order_date,
    orders.total_amount
FROM customers
INNER JOIN orders ON customers.id = orders.customer_id;

-- Using table aliases (recommended)
SELECT 
    c.first_name,
    c.last_name,
    o.order_date,
    o.total_amount
FROM customers c
INNER JOIN orders o ON c.id = o.customer_id;

-- Multiple joins
SELECT 
    c.first_name,
    c.last_name,
    p.product_name,
    oi.quantity,
    oi.unit_price
FROM customers c
INNER JOIN orders o ON c.id = o.customer_id
INNER JOIN order_items oi ON o.id = oi.order_id
INNER JOIN products p ON oi.product_id = p.id;
```

### LEFT JOIN (LEFT OUTER JOIN)

Returns all rows from the left table and matching rows from the right table.

```sql
-- All customers and their orders (including customers with no orders)
SELECT 
    c.first_name,
    c.last_name,
    o.order_date,
    o.total_amount
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id;

-- Find customers who haven't placed orders
SELECT 
    c.first_name,
    c.last_name
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
WHERE o.id IS NULL;
```

### RIGHT JOIN (RIGHT OUTER JOIN)

Returns all rows from the right table and matching rows from the left table.

```sql
-- All orders and customer info (including orders without customer data)
SELECT 
    o.order_date,
    o.total_amount,
    c.first_name,
    c.last_name
FROM customers c
RIGHT JOIN orders o ON c.id = o.customer_id;
```

### FULL OUTER JOIN

Returns all rows when there's a match in either table.

```sql
-- All customers and orders (SQLite doesn't support this, but PostgreSQL/MySQL do)
SELECT 
    c.first_name,
    c.last_name,
    o.order_date
FROM customers c
FULL OUTER JOIN orders o ON c.id = o.customer_id;
```

### CROSS JOIN

Returns the Cartesian product of both tables.

```sql
-- Every combination of customers and products
SELECT 
    c.first_name,
    p.product_name
FROM customers c
CROSS JOIN products p;
```

### SELF JOIN

Join a table to itself.

```sql
-- Employees and their managers (if you had an employees table)
SELECT 
    e.first_name AS employee_name,
    m.first_name AS manager_name
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;

-- Find customers from the same city
SELECT 
    c1.first_name AS customer1,
    c2.first_name AS customer2,
    c1.city
FROM customers c1
INNER JOIN customers c2 ON c1.city = c2.city AND c1.id < c2.id;
```

### Practice Exercises - Module 4

1. List all products with their category names
2. Show all orders with customer names and email addresses
3. Find customers who have never placed an order
4. Display order details with product names and quantities
5. List all products and show how many times each has been ordered (include products never ordered)

---

## Module 5: Subqueries

Subqueries are queries nested inside another query.

### Subquery in WHERE Clause

```sql
-- Find products more expensive than average
SELECT product_name, price
FROM products
WHERE price > (SELECT AVG(price) FROM products);

-- Customers who placed orders
SELECT first_name, last_name
FROM customers
WHERE id IN (SELECT DISTINCT customer_id FROM orders);

-- Products never ordered
SELECT product_name
FROM products
WHERE id NOT IN (SELECT DISTINCT product_id FROM order_items);
```

### Subquery in SELECT Clause

```sql
-- Show each customer with their total number of orders
SELECT 
    first_name,
    last_name,
    (SELECT COUNT(*) 
     FROM orders 
     WHERE customer_id = customers.id) AS order_count
FROM customers;

-- Products with their total sales
SELECT 
    product_name,
    price,
    (SELECT SUM(quantity) 
     FROM order_items 
     WHERE product_id = products.id) AS total_sold
FROM products;
```

### Subquery in FROM Clause (Derived Tables)

```sql
-- Average order value per customer
SELECT 
    customer_id,
    AVG(total_amount) AS avg_order_value
FROM (
    SELECT customer_id, total_amount
    FROM orders
    WHERE status = 'completed'
) AS completed_orders
GROUP BY customer_id;

-- Top 5 customers by revenue
SELECT c.first_name, c.last_name, customer_totals.revenue
FROM (
    SELECT customer_id, SUM(total_amount) AS revenue
    FROM orders
    GROUP BY customer_id
    ORDER BY revenue DESC
    LIMIT 5
) AS customer_totals
JOIN customers c ON customer_totals.customer_id = c.id;
```

### Correlated Subqueries

Subquery references the outer query.

```sql
-- Products with above-average price in their category
SELECT p1.product_name, p1.price, p1.category_id
FROM products p1
WHERE p1.price > (
    SELECT AVG(p2.price)
    FROM products p2
    WHERE p2.category_id = p1.category_id
);

-- Customers with above-average order count
SELECT first_name, last_name
FROM customers c
WHERE (
    SELECT COUNT(*)
    FROM orders o
    WHERE o.customer_id = c.id
) > (
    SELECT AVG(order_count)
    FROM (
        SELECT COUNT(*) AS order_count
        FROM orders
        GROUP BY customer_id
    ) AS counts
);
```

### EXISTS and NOT EXISTS

```sql
-- Customers who have placed orders
SELECT first_name, last_name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.id
);

-- Products that have never been ordered
SELECT product_name
FROM products p
WHERE NOT EXISTS (
    SELECT 1
    FROM order_items oi
    WHERE oi.product_id = p.id
);
```

### Practice Exercises - Module 5

1. Find products cheaper than the average price in their category
2. List customers who spent more than $500 total
3. Show products that were ordered more frequently than the average
4. Find the second highest priced product
5. Get customers who ordered in both January and February 2024

---

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

### Practice Exercises - Module 6

1. Insert 3 new customers into the database
2. Update all products in category 2 with a 15% price increase
3. Delete all orders older than 2 years
4. Create a transaction that transfers inventory from one product to another
5. Update customer email addresses to lowercase

---

## Module 7: Advanced Queries

### Common Table Expressions (CTEs)

CTEs make complex queries more readable.

```sql
-- Basic CTE
WITH expensive_products AS (
    SELECT product_name, price
    FROM products
    WHERE price > 100
)
SELECT * FROM expensive_products
ORDER BY price DESC;

-- Multiple CTEs
WITH 
customer_totals AS (
    SELECT 
        customer_id,
        SUM(total_amount) AS total_spent
    FROM orders
    GROUP BY customer_id
),
high_value_customers AS (
    SELECT customer_id
    FROM customer_totals
    WHERE total_spent > 1000
)
SELECT c.first_name, c.last_name, ct.total_spent
FROM customers c
JOIN customer_totals ct ON c.id = ct.customer_id
JOIN high_value_customers hvc ON c.id = hvc.customer_id;

-- Recursive CTE (for hierarchical data)
WITH RECURSIVE category_tree AS (
    -- Anchor: top-level categories
    SELECT id, name, parent_id, 0 AS level
    FROM categories
    WHERE parent_id IS NULL
    
    UNION ALL
    
    -- Recursive: child categories
    SELECT c.id, c.name, c.parent_id, ct.level + 1
    FROM categories c
    JOIN category_tree ct ON c.parent_id = ct.id
)
SELECT * FROM category_tree ORDER BY level, name;
```

### Window Functions

Perform calculations across rows related to the current row.

**ROW_NUMBER, RANK, DENSE_RANK:**
```sql
-- Assign row numbers
SELECT 
    product_name,
    price,
    ROW_NUMBER() OVER (ORDER BY price DESC) AS row_num,
    RANK() OVER (ORDER BY price DESC) AS rank,
    DENSE_RANK() OVER (ORDER BY price DESC) AS dense_rank
FROM products;

-- Rank within groups
SELECT 
    category_id,
    product_name,
    price,
    RANK() OVER (PARTITION BY category_id ORDER BY price DESC) AS rank_in_category
FROM products;
```

**Aggregates with OVER:**
```sql
-- Running total
SELECT 
    order_date,
    total_amount,
    SUM(total_amount) OVER (ORDER BY order_date) AS running_total
FROM orders;

-- Moving average
SELECT 
    order_date,
    total_amount,
    AVG(total_amount) OVER (
        ORDER BY order_date 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS moving_avg_7days
FROM orders;
```

**LAG and LEAD:**
```sql
-- Compare with previous row
SELECT 
    order_date,
    total_amount,
    LAG(total_amount, 1) OVER (ORDER BY order_date) AS previous_day,
    total_amount - LAG(total_amount, 1) OVER (ORDER BY order_date) AS difference
FROM daily_sales;

-- Compare with next row
SELECT 
    product_name,
    price,
    LEAD(price, 1) OVER (ORDER BY price) AS next_price
FROM products;
```

### CASE Statements

```sql
-- Simple CASE
SELECT 
    product_name,
    price,
    CASE 
        WHEN price < 20 THEN 'Budget'
        WHEN price BETWEEN 20 AND 100 THEN 'Mid-range'
        ELSE 'Premium'
    END AS price_category
FROM products;

-- CASE in aggregation
SELECT 
    category_id,
    COUNT(*) AS total_products,
    COUNT(CASE WHEN price < 50 THEN 1 END) AS affordable_count,
    COUNT(CASE WHEN price >= 50 THEN 1 END) AS expensive_count
FROM products
GROUP BY category_id;

-- Conditional aggregation
SELECT 
    SUM(CASE WHEN status = 'completed' THEN total_amount ELSE 0 END) AS completed_revenue,
    SUM(CASE WHEN status = 'pending' THEN total_amount ELSE 0 END) AS pending_revenue,
    SUM(CASE WHEN status = 'cancelled' THEN total_amount ELSE 0 END) AS cancelled_revenue
FROM orders;
```

### String Functions

```sql
-- Concatenation
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM customers;

-- Alternative: || operator
SELECT first_name || ' ' || last_name AS full_name
FROM customers;

-- Upper and lower case
SELECT 
    UPPER(product_name) AS uppercase,
    LOWER(product_name) AS lowercase
FROM products;

-- Substring
SELECT SUBSTRING(email, 1, POSITION('@' IN email) - 1) AS username
FROM customers;

-- Trimming
SELECT TRIM('  extra spaces  ') AS trimmed;

-- Replace
SELECT REPLACE(phone, '-', '') AS phone_no_dashes
FROM customers;

-- Length
SELECT product_name, LENGTH(product_name) AS name_length
FROM products;
```

### Date Functions

```sql
-- Current date/time
SELECT 
    CURRENT_DATE,
    CURRENT_TIME,
    CURRENT_TIMESTAMP;

-- Extract parts
SELECT 
    order_date,
    EXTRACT(YEAR FROM order_date) AS year,
    EXTRACT(MONTH FROM order_date) AS month,
    EXTRACT(DAY FROM order_date) AS day
FROM orders;

-- Date arithmetic
SELECT 
    order_date,
    order_date + INTERVAL '30 days' AS due_date,
    CURRENT_DATE - order_date AS days_since_order
FROM orders;

-- Format dates
SELECT 
    TO_CHAR(order_date, 'YYYY-MM-DD') AS formatted_date,
    TO_CHAR(order_date, 'Month DD, YYYY') AS readable_date
FROM orders;

-- Date truncation
SELECT 
    DATE_TRUNC('month', order_date) AS month_start,
    COUNT(*) AS orders_per_month
FROM orders
GROUP BY DATE_TRUNC('month', order_date);
```

### UNION, INTERSECT, EXCEPT

```sql
-- UNION (removes duplicates)
SELECT city FROM customers
UNION
SELECT city FROM suppliers;

-- UNION ALL (keeps duplicates)
SELECT product_name FROM products WHERE category_id = 1
UNION ALL
SELECT product_name FROM products WHERE category_id = 2;

-- INTERSECT (common values)
SELECT customer_id FROM orders WHERE EXTRACT(MONTH FROM order_date) = 1
INTERSECT
SELECT customer_id FROM orders WHERE EXTRACT(MONTH FROM order_date) = 2;

-- EXCEPT (in first but not second)
SELECT customer_id FROM customers
EXCEPT
SELECT customer_id FROM orders;
```

### Practice Exercises - Module 7

1. Create a CTE to find the top 3 products by revenue, then join with product details
2. Use window functions to rank customers by total spending
3. Calculate a 7-day moving average of daily sales
4. Create price categories (Low, Medium, High) using CASE
5. Find customers who placed orders in consecutive months

---

## Module 8: Database Design

### Normalization

**First Normal Form (1NF):**
- Each column contains atomic values
- No repeating groups

❌ Bad:
```
customers
+----+-----------+----------------------+
| id | name      | phones               |
+----+-----------+----------------------+
| 1  | John Doe  | 555-1234, 555-5678   |
+----+-----------+----------------------+
```

✅ Good:
```
customers              customer_phones
+----+-----------+     +-------------+-------+------------+
| id | name      |     | customer_id | id    | phone      |
+----+-----------+     +-------------+-------+------------+
| 1  | John Doe  |     | 1           | 1     | 555-1234   |
+----+-----------+     | 1           | 2     | 555-5678   |
                       +-------------+-------+------------+
```

**Second Normal Form (2NF):**
- Meet 1NF
- No partial dependencies (all non-key columns depend on entire primary key)

**Third Normal Form (3NF):**
- Meet 2NF
- No transitive dependencies (non-key columns don't depend on other non-key columns)

### Primary Keys and Foreign Keys

```sql
-- Create table with primary key
CREATE TABLE customers (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create table with foreign key
CREATE TABLE orders (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    customer_id INTEGER NOT NULL,
    order_date DATE NOT NULL,
    total_amount DECIMAL(10, 2),
    status VARCHAR(20) DEFAULT 'pending',
    FOREIGN KEY (customer_id) REFERENCES customers(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- Composite primary key
CREATE TABLE order_items (
    order_id INTEGER,
    product_id INTEGER,
    quantity INTEGER NOT NULL,
    unit_price DECIMAL(10, 2) NOT NULL,
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

### Constraints

```sql
CREATE TABLE products (
    id INTEGER PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    sku VARCHAR(50) UNIQUE NOT NULL,
    price DECIMAL(10, 2) CHECK (price >= 0),
    stock_quantity INTEGER DEFAULT 0 CHECK (stock_quantity >= 0),
    category_id INTEGER,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id)
);
```

### Indexes

```sql
-- Create index
CREATE INDEX idx_customers_email ON customers(email);

-- Create composite index
CREATE INDEX idx_orders_customer_date ON orders(customer_id, order_date);

-- Create unique index
CREATE UNIQUE INDEX idx_products_sku ON products(sku);

-- Drop index
DROP INDEX idx_customers_email;

-- View indexes
SHOW INDEX FROM customers;
```

### Views

```sql
-- Create view
CREATE VIEW customer_orders AS
SELECT 
    c.id AS customer_id,
    c.first_name,
    c.last_name,
    o.id AS order_id,
    o.order_date,
    o.total_amount
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id;

-- Use view
SELECT * FROM customer_orders WHERE order_date > '2024-01-01';

-- Create materialized view (PostgreSQL)
CREATE MATERIALIZED VIEW product_sales_summary AS
SELECT 
    p.id,
    p.product_name,
    COUNT(oi.order_id) AS times_ordered,
    SUM(oi.quantity) AS total_quantity,
    SUM(oi.quantity * oi.unit_price) AS total_revenue
FROM products p
LEFT JOIN order_items oi ON p.id = oi.product_id
GROUP BY p.id, p.product_name;

-- Refresh materialized view
REFRESH MATERIALIZED VIEW product_sales_summary;
```

### Practice Exercises - Module 8

1. Design a database schema for a blog (users, posts, comments, tags)
2. Create a table with appropriate constraints for a product inventory
3. Create indexes to optimize common queries
4. Create a view that shows order summaries with customer information
5. Normalize a denormalized table structure

---

## Module 9: Performance Optimization

### EXPLAIN - Query Execution Plan

```sql
-- Analyze query performance
EXPLAIN SELECT * FROM orders WHERE customer_id = 100;

-- More detailed analysis
EXPLAIN ANALYZE SELECT * FROM orders WHERE customer_id = 100;
```

### Index Optimization

```sql
-- Good: Using index
SELECT * FROM customers WHERE email = 'john@email.com';

-- Bad: Function on indexed column (can't use index)
SELECT * FROM customers WHERE UPPER(email) = 'JOHN@EMAIL.COM';

-- Better: Store normalized data or use functional index
CREATE INDEX idx_customers_email_upper ON customers(UPPER(email));

-- Covering index (includes all needed columns)
CREATE INDEX idx_orders_covering ON orders(customer_id, order_date, total_amount);
```

### Query Optimization Techniques

**1. Select only needed columns:**
```sql
-- Bad
SELECT * FROM products;

-- Good
SELECT id, product_name, price FROM products;
```

**2. Use EXISTS instead of IN for large datasets:**
```sql
-- Slower for large datasets
SELECT * FROM customers 
WHERE id IN (SELECT customer_id FROM orders);

-- Faster
SELECT * FROM customers c
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.id);
```

**3. Avoid SELECT DISTINCT when possible:**
```sql
-- Slower
SELECT DISTINCT customer_id FROM orders;

-- Faster if you just need existence
SELECT customer_id FROM orders GROUP BY customer_id;
```

**4. Use LIMIT for large result sets:**
```sql
-- Pagination
SELECT * FROM products 
ORDER BY created_at DESC 
LIMIT 20 OFFSET 0;
```

**5. Optimize JOINs:**
```sql
-- Bad: Joining large tables without filtering
SELECT * FROM orders o
JOIN customers c ON o.customer_id = c.id;

-- Better: Filter first
SELECT * FROM orders o
JOIN customers c ON o.customer_id = c.id
WHERE o.order_date >= '2024-01-01';
```

### Database Maintenance

```sql
-- Update statistics (PostgreSQL)
ANALYZE customers;

-- Vacuum (PostgreSQL - reclaim space)
VACUUM customers;

-- Optimize table (MySQL)
OPTIMIZE TABLE customers;

-- Rebuild index
REINDEX INDEX idx_customers_email;
```

### Practice Exercises - Module 9

1. Use EXPLAIN to analyze a slow query and optimize it
2. Create appropriate indexes for a set of common queries
3. Rewrite a query with multiple subqueries using JOINs
4. Optimize a query that selects all columns but only needs a few
5. Compare performance of IN vs EXISTS on a large dataset

---

## Module 10: Real-World Projects

### Project 1: E-Commerce Sales Analysis

**Requirements:**
1. Top 10 best-selling products
2. Monthly revenue trends
3. Customer lifetime value
4. Product categories performance
5. Customers who haven't purchased in 90 days

**Sample Solutions:**

```sql
-- 1. Top 10 best-selling products
SELECT 
    p.product_name,
    SUM(oi.quantity) AS total_sold,
    SUM(oi.quantity * oi.unit_price) AS revenue
FROM products p
JOIN order_items oi ON p.id = oi.product_id
GROUP BY p.id, p.product_name
ORDER BY total_sold DESC
LIMIT 10;

-- 2. Monthly revenue trends
SELECT 
    DATE_TRUNC('month', order_date) AS month,
    COUNT(*) AS order_count,
    SUM(total_amount) AS revenue,
    AVG(total_amount) AS avg_order_value
FROM orders
WHERE status = 'completed'
GROUP BY DATE_TRUNC('month', order_date)
ORDER BY month;

-- 3. Customer lifetime value
SELECT 
    c.id,
    c.first_name,
    c.last_name,
    COUNT(o.id) AS order_count,
    SUM(o.total_amount) AS lifetime_value,
    AVG(o.total_amount) AS avg_order_value,
    MAX(o.order_date) AS last_order_date
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
GROUP BY c.id, c.first_name, c.last_name
ORDER BY lifetime_value DESC;

-- 4. Category performance
SELECT 
    cat.name AS category,
    COUNT(DISTINCT p.id) AS product_count,
    COUNT(DISTINCT oi.order_id) AS orders,
    SUM(oi.quantity) AS units_sold,
    SUM(oi.quantity * oi.unit_price) AS revenue
FROM categories cat
LEFT JOIN products p ON cat.id = p.category_id
LEFT JOIN order_items oi ON p.id = oi.product_id
GROUP BY cat.id, cat.name
ORDER BY revenue DESC;

-- 5. Dormant customers (no purchase in 90 days)
SELECT 
    c.id,
    c.first_name,
    c.last_name,
    c.email,
    MAX(o.order_date) AS last_order_date,
    CURRENT_DATE - MAX(o.order_date) AS days_since_order
FROM customers c
JOIN orders o ON c.id = o.customer_id
GROUP BY c.id, c.first_name, c.last_name, c.email
HAVING MAX(o.order_date) < CURRENT_DATE - INTERVAL '90 days'
ORDER BY days_since_order DESC;
```

### Project 2: Customer Segmentation

Create RFM (Recency, Frequency, Monetary) analysis:

```sql
WITH rfm_calc AS (
    SELECT 
        customer_id,
        CURRENT_DATE - MAX(order_date) AS recency,
        COUNT(*) AS frequency,
        SUM(total_amount) AS monetary
    FROM orders
    WHERE status = 'completed'
    GROUP BY customer_id
),
rfm_scores AS (
    SELECT 
        customer_id,
        recency,
        frequency,
        monetary,
        NTILE(5) OVER (ORDER BY recency DESC) AS r_score,
        NTILE(5) OVER (ORDER BY frequency) AS f_score,
        NTILE(5) OVER (ORDER BY monetary) AS m_score
    FROM rfm_calc
)
SELECT 
    c.first_name,
    c.last_name,
    rs.recency,
    rs.frequency,
    rs.monetary,
    rs.r_score || rs.f_score || rs.m_score AS rfm_segment,
    CASE 
        WHEN rs.r_score >= 4 AND rs.f_score >= 4 THEN 'Champions'
        WHEN rs.r_score >= 3 AND rs.f_score >= 3 THEN 'Loyal'
        WHEN rs.r_score >= 4 AND rs.f_score <= 2 THEN 'New Customers'
        WHEN rs.r_score <= 2 AND rs.f_score >= 3 THEN 'At Risk'
        WHEN rs.r_score <= 2 AND rs.f_score <= 2 THEN 'Lost'
        ELSE 'Regular'
    END AS segment_name
FROM rfm_scores rs
JOIN customers c ON rs.customer_id = c.id
ORDER BY monetary DESC;
```

### Project 3: Inventory Management

```sql
-- Low stock alert
SELECT 
    p.product_name,
    p.stock_quantity,
    COALESCE(AVG(oi.quantity), 0) AS avg_daily_sales,
    CASE 
        WHEN COALESCE(AVG(oi.quantity), 0) > 0 
        THEN p.stock_quantity / AVG(oi.quantity)
        ELSE NULL
    END AS days_until_stockout
FROM products p
LEFT JOIN order_items oi ON p.id = oi.product_id
LEFT JOIN orders o ON oi.order_id = o.id 
    AND o.order_date >= CURRENT_DATE - INTERVAL '30 days'
GROUP BY p.id, p.product_name, p.stock_quantity
HAVING p.stock_quantity < 20 OR 
       (COALESCE(AVG(oi.quantity), 0) > 0 AND 
        p.stock_quantity / AVG(oi.quantity) < 7)
ORDER BY days_until_stockout;
```

### Practice Projects

1. **User Activity Dashboard**: Track daily/weekly/monthly active users
2. **Cohort Analysis**: Analyze customer retention by signup month
3. **Product Recommendation Engine**: Find frequently bought together items
4. **Sales Forecasting**: Calculate trends and growth rates
5. **Churn Prediction**: Identify customers likely to stop purchasing

---

## Bonus: Best Practices & Tips

### SQL Style Guide

```sql
-- Use consistent naming conventions
-- Tables: plural, lowercase with underscores
-- Columns: lowercase with underscores
-- Aliases: meaningful and short

-- Good formatting
SELECT 
    c.first_name,
    c.last_name,
    COUNT(o.id) AS order_count,
    SUM(o.total_amount) AS total_spent
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
WHERE c.created_at >= '2024-01-01'
GROUP BY c.id, c.first_name, c.last_name
HAVING COUNT(o.id) > 5
ORDER BY total_spent DESC;
```

### Common Mistakes to Avoid

1. **Not using proper JOINs**
```sql
-- Bad (Cartesian product)
SELECT * FROM customers, orders;

-- Good
SELECT * FROM customers c
JOIN orders o ON c.id = o.customer_id;
```

2. **Comparing NULL with =**
```sql
-- Wrong
WHERE column = NULL

-- Correct
WHERE column IS NULL
```

3. **Not considering NULLs in calculations**
```sql
-- May give unexpected results
SELECT AVG(rating) FROM products;  -- Ignores NULLs

-- Be explicit
SELECT AVG(COALESCE(rating, 0)) FROM products;
```

4. **Using SELECT * in production code**
```sql
-- Bad (wasteful, fragile)
SELECT * FROM large_table;

-- Good
SELECT id, name, price FROM large_table;
```

### Security Best Practices

```sql
-- NEVER do this (SQL injection vulnerable):
query = "SELECT * FROM users WHERE username = '" + user_input + "'"

-- Use parameterized queries:
-- Python example
cursor.execute("SELECT * FROM users WHERE username = ?", (user_input,))

-- Grant minimal permissions
GRANT SELECT ON products TO read_only_user;
REVOKE ALL ON customers FROM public;
```

### Learning Resources

- **Practice Platforms**: LeetCode, HackerRank, SQLZoo, Mode Analytics
- **Documentation**: PostgreSQL docs, MySQL docs, SQLite docs
- **Sample Databases**: Chinook, AdventureWorks, Northwind
- **Books**: "SQL Performance Explained" by Markus Winand

---

## Conclusion

You've completed the SQL Bootcamp! You now have skills ranging from basic queries to complex analytics and database design. 

**Next Steps:**
1. Practice regularly with real datasets
2. Work on personal projects
3. Contribute to open-source projects
4. Learn specific database systems deeply (PostgreSQL, MySQL, etc.)
5. Explore advanced topics: query optimization, replication, sharding

**Remember:**
- SQL is a skill that improves with practice
- Every database is slightly different—check documentation
- Performance matters—always think about how your queries scale
- Clean, readable code is professional code

Happy querying! 🚀
