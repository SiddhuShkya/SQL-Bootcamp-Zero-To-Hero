### E-Commerce Sales Analysis

**Requirements:**
1. Top 10 best-selling products
2. Monthly revenue trends
3. Customer lifetime value
4. Product categories performance
5. Customers who haven't purchased in 90 days

**Sample Solutions:**

```postgresql
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