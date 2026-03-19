## Module 8: Database Design

### Normalization

**First Normal Form (1NF):**
- Each column contains atomic values
- No repeating groups

❌ Bad:
```
customers
+----+-----------+----------------------+
| id | name      | phones               |
+----+-----------+----------------------+
| 1  | John Doe  | 555-1234, 555-5678   |
+----+-----------+----------------------+
```

✅ Good:
```
customers              customer_phones
+----+-----------+     +-------------+-------+------------+
| id | name      |     | customer_id | id    | phone      |
+----+-----------+     +-------------+-------+------------+
| 1  | John Doe  |     | 1           | 1     | 555-1234   |
+----+-----------+     | 1           | 2     | 555-5678   |
                       +-------------+-------+------------+
```

**Second Normal Form (2NF):**
- Meet 1NF
- No partial dependencies (all non-key columns depend on entire primary key)

**Third Normal Form (3NF):**
- Meet 2NF
- No transitive dependencies (non-key columns don't depend on other non-key columns)

### Primary Keys and Foreign Keys

```sql
-- Create table with primary key
CREATE TABLE customers (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create table with foreign key
CREATE TABLE orders (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    customer_id INTEGER NOT NULL,
    order_date DATE NOT NULL,
    total_amount DECIMAL(10, 2),
    status VARCHAR(20) DEFAULT 'pending',
    FOREIGN KEY (customer_id) REFERENCES customers(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- Composite primary key
CREATE TABLE order_items (
    order_id INTEGER,
    product_id INTEGER,
    quantity INTEGER NOT NULL,
    unit_price DECIMAL(10, 2) NOT NULL,
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

### Constraints

```sql
CREATE TABLE products (
    id INTEGER PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    sku VARCHAR(50) UNIQUE NOT NULL,
    price DECIMAL(10, 2) CHECK (price >= 0),
    stock_quantity INTEGER DEFAULT 0 CHECK (stock_quantity >= 0),
    category_id INTEGER,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id)
);
```

### Indexes

```sql
-- Create index
CREATE INDEX idx_customers_email ON customers(email);

-- Create composite index
CREATE INDEX idx_orders_customer_date ON orders(customer_id, order_date);

-- Create unique index
CREATE UNIQUE INDEX idx_products_sku ON products(sku);

-- Drop index
DROP INDEX idx_customers_email;

-- View indexes
SHOW INDEX FROM customers;
```

### Views

```sql
-- Create view
CREATE VIEW customer_orders AS
SELECT 
    c.id AS customer_id,
    c.first_name,
    c.last_name,
    o.id AS order_id,
    o.order_date,
    o.total_amount
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id;

-- Use view
SELECT * FROM customer_orders WHERE order_date > '2024-01-01';

-- Create materialized view (PostgreSQL)
CREATE MATERIALIZED VIEW product_sales_summary AS
SELECT 
    p.id,
    p.product_name,
    COUNT(oi.order_id) AS times_ordered,
    SUM(oi.quantity) AS total_quantity,
    SUM(oi.quantity * oi.unit_price) AS total_revenue
FROM products p
LEFT JOIN order_items oi ON p.id = oi.product_id
GROUP BY p.id, p.product_name;

-- Refresh materialized view
REFRESH MATERIALIZED VIEW product_sales_summary;
```