### Customer Segmentation

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