## Module 1: SQL Fundamentals

### Understanding Databases

A database is an organized collection of data. Tables are the foundation:

```
Table: customers
+----+------------+-----------+------------------+
| id | first_name | last_name | email            |
+----+------------+-----------+------------------+
| 1  | John       | Doe       | john@email.com   |
| 2  | Jane       | Smith     | jane@email.com   |
+----+------------+-----------+------------------+
```

### SELECT Statement - Your First Query

The `SELECT` statement retrieves data from a database.

**Basic Syntax:**
```sql
SELECT column1, column2
FROM table_name;
```

**Examples:**

```sql
-- Select all columns
SELECT * FROM customers;

-- Select specific columns
SELECT first_name, email FROM customers;

-- Select with alias (renaming columns)
SELECT 
    first_name AS "First Name",
    last_name AS "Last Name"
FROM customers;
```

### DISTINCT - Removing Duplicates

```sql
-- Get unique cities
SELECT DISTINCT city FROM customers;

-- Get unique combinations
SELECT DISTINCT city, state FROM customers;
```