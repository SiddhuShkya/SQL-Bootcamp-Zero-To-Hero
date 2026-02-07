## Challenge Tasks

This document will contain all the challenges that were presented to me for a better learning experience. Challenges are structured in the below manners:

- Business Situation
- Challenge Question
- Expected Answer
- Hints
- Solution

---

### 1. SELECT 

- `Business Situation` : We want to send out promotional email to our existing customers!

- `Challenge` : Use a SELECT statement to grab the first and last names of every cutsomers and their email addresses.

- `Expected Answer`: 

| first_name | last_name | email |
|------------|-----------|-------|
| Jared | Ely | jared.ely@sakilacustomer.org |
| Mary | Smith | mary.smith@sakilacustomer.org |
| Patricia | Johnson | patricia.johnson@sakilacustomer.org |
| Linda | Williams | linda.williams@sakilacustomer.org |
| Barbara | Jones | barbara.jones@sakilacustomer.org |
| ... | ... | ... |

- Hints:
    - Use the `customer` table
    - You can use the table drop-down to view what columns are available
    - You could also use SELECT * FROM `customer` to see all then columns

- Solutions

    - View all columns from `customer` table

    ```sql
    SELECT * FROM customer;
    ```
    | customer_id | store_id | first_name | last_name | email | address_id | activebool | create_date | last_update | active |
    |-------------|----------|------------|-----------|-------|------------|------------|-------------|-------------|--------|
    | 524 | 1 | Jared | Ely | jared.ely@sakilacustomer.org | 530 | True | 2006-02-14 | 2013-05-26 14:49:45.738 | 1 |
    | 1 | 1 | Mary | Smith | mary.smith@sakilacustomer.org | 5 | True | 2006-02-14 | 2013-05-26 14:49:45.738 | 1 |
    | 2 | 1 | Patricia | Johnson | patricia.johnson@sakilacustomer.org | 6 | True | 2006-02-14 | 2013-05-26 14:49:45.738 | 1 |
    | 3 | 1 | Linda | Williams | linda.williams@sakilacustomer.org | 7 | True | 2006-02-14 | 2013-05-26 14:49:45.738 | 1 |
    | 4 | 2 | Barbara | Jones | barbara.jones@sakilacustomer.org | 8 | True | 2006-02-14 | 2013-05-26 14:49:45.738 | 1 |

    - View first_name, last_name, email from `customer`

    ```sql
    SELECT first_name, last_name, email FROM customer;
    ```
    | first_name | last_name | email |
    |------------|-----------|-------|
    | Jared | Ely | jared.ely@sakilacustomer.org |
    | Mary | Smith | mary.smith@sakilacustomer.org |
    | Patricia | Johnson | patricia.johnson@sakilacustomer.org |
    | Linda | Williams | linda.williams@sakilacustomer.org |
    | Barbara | Jones | barbara.jones@sakilacustomer.org |

---

### 2. SELECT DISTINCT