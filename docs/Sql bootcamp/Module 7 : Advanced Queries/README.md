## Module 7: Advanced Queries

### Common Table Expressions (CTEs)

CTEs make complex queries more readable.

```postgresql
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
```postgresql
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
```postgresql
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
```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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