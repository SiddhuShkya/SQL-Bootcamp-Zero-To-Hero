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