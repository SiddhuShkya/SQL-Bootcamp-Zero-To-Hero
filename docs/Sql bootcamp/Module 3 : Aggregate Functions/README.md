## Module 3: Aggregate Functions

### COUNT - Counting Rows

```postgresql
-- Count all rows
SELECT COUNT(*) FROM customers;

-- Count non-null values
SELECT COUNT(phone) FROM customers;

-- Count distinct values
SELECT COUNT(DISTINCT city) FROM customers;
```

### SUM - Adding Values

```postgresql
-- Total revenue
SELECT SUM(total_amount) FROM orders;

-- Total quantity ordered
SELECT SUM(quantity) FROM order_items;
```

### AVG - Average Values

```postgresql
-- Average product price
SELECT AVG(price) FROM products;

-- Average order value
SELECT AVG(total_amount) FROM orders;
```

### MIN and MAX

```postgresql
-- Cheapest and most expensive products
SELECT 
    MIN(price) AS cheapest,
    MAX(price) AS most_expensive
FROM products;
```

### GROUP BY - Grouping Data

Group rows that have the same values and apply aggregate functions.

```postgresql
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

```postgresql
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