### Inventory Management

```postgresql
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