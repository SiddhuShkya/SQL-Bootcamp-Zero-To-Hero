## Module 4: Joins

Joins combine rows from two or more tables based on related columns.

### INNER JOIN

Returns only matching rows from both tables.

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
-- Every combination of customers and products
SELECT 
    c.first_name,
    p.product_name
FROM customers c
CROSS JOIN products p;
```

### SELF JOIN

Join a table to itself.

```postgresql
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