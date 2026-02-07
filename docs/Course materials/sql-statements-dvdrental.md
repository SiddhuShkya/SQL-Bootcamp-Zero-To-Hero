## SQL Statements Using dvdrental database

This document contains all the sql statements/queries we executed for this course using the postgresql and pgadmin from the dvdrental datbase.

> Open up your PgAdmin. Then connect your Local DB server and open up your Query tool from the dvdrental database

<img src="../../images/dvdrental-querytool.png"
    alt="Image Caption"
    style="border:1px solid white; padding:1px; background:#fff; width: 3000px;" />

> See the tables that are present in the dvdrental database.

> [!IMPORTANT]
> You can see the tables that inside the database by extending: database (dvdrental) -> Schemas -> Public -> Tables. Similarly you can extend a specific table to also see their columns.

<img src="../../images/database-tables.png"
    alt="Image Caption"
    style="border:1px solid white; padding:1px; background:#fff; width: 3000px;" />

> We have the following 15 available tables in our dvdrental database

- actor 
- address 
- category 
- city 
- country 
- customer 
- film
- film_actor
- film_category
- inventory
- language
- payment
- rental
- staff
- store

*Now that we know all the tables that are inside dvdrental database, let's move forward write some SQL queries to retrieve some informations*

---

### 1. SQL Statement Fundamentals

1.1 **SELECT** 

- View all columns from `actor`

```sql
SELECT * FROM actor;
```
| actor_id | first_name | last_name | last_update |
|----------|------------|-----------|-------------|
| 1 | Penelope | Guiness | 2013-05-26 14:47:57.62 |
| 2 | Nick | Wahlberg | 2013-05-26 14:47:57.62 |
| 3 | Ed | Chase | 2013-05-26 14:47:57.62 |
| 4 | Jennifer | Davis | 2013-05-26 14:47:57.62 |
| 5 | Johnny | Lollobrigida | 2013-05-26 14:47:57.62 |

> Returns all the columns from the `actor` table

- View only one column from `actor`

```sql
SELECT first_name FROM actor;
```
| first_name |
|------------|
| Penelope |
| Nick |
| Ed |
| Jennifer |
| Johnny |

> Returns only the first_name column from the `actor` table

- View first_name and last_name from `actor` table

```sql
SELECT first_name, last_name FROM actor;
```
| first_name | last_name |
|------------|-----------|
| Penelope | Guiness |
| Nick | Wahlberg |
| Ed | Chase |
| Jennifer | Davis |
| Johnny | Lollobrigida |

> Returns first_name and last_name from `actor` table

> [!NOTE]
> The order of the column names matters in the query as it determines the order of columns in the result set. [SELECT last_name, first_name] will display last_name in the first column and first_name in the second column.

1.2 **SELECT DISTINCT**

