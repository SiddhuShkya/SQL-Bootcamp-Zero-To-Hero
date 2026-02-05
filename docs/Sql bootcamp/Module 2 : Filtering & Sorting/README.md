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