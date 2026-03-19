## Module 5: Subqueries

Subqueries are queries nested inside another query.

### Subquery in WHERE Clause

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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