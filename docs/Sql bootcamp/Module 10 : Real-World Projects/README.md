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