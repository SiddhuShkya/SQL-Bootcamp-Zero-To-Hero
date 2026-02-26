##  Aggregate Functions & GROUP BY Statements 

This document contains all the sql **AS** and **JOINS** statements, we executed for this course using the postgresql and pgadmin from the dvdrental datbase.

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

### 1. AS

> Explore the `payment` table.

```sql
SELECT * FROM payment
LIMIT 5;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>payment_id</th>
      <th>customer_id</th>
      <th>staff_id</th>
      <th>rental_id</th>
      <th>amount</th>
      <th>payment_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>17503</td>
      <td>341</td>
      <td>2</td>
      <td>1520</td>
      <td>7.99</td>
      <td>2007-02-15 22:25:46.996577</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17504</td>
      <td>341</td>
      <td>1</td>
      <td>1778</td>
      <td>1.99</td>
      <td>2007-02-16 17:23:14.996577</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17505</td>
      <td>341</td>
      <td>1</td>
      <td>1849</td>
      <td>7.99</td>
      <td>2007-02-16 22:41:45.996577</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17506</td>
      <td>341</td>
      <td>2</td>
      <td>2829</td>
      <td>2.99</td>
      <td>2007-02-19 19:39:56.996577</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17507</td>
      <td>341</td>
      <td>2</td>
      <td>3130</td>
      <td>7.99</td>
      <td>2007-02-20 17:31:48.996577</td>
    </tr>
  </tbody>
</table>

> View the total number of transactions made, and clarify the result using an alias.

```sql
SELECT COUNT(*) AS num_transactions FROM payment;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>num_transactions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>14596</td>
    </tr>
  </tbody>
</table>

The result column has been renamed to 'num_transactions' from 'COUNT(*)', calrifying our result.

> View how much each customer has spend.

```sql
SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>SUM(amount)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>114.70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>123.74</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>130.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>81.78</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>134.65</td>
    </tr>
  </tbody>
</table>

> Use an alias to clarify the above result.

```sql
SELECT customer_id, SUM(amount) AS total_spent FROM payment
GROUP BY customer_id;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>total_spent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>114.70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>123.74</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>130.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>81.78</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>134.65</td>
    </tr>
  </tbody>
</table>

> Filter the above result, only display those whos total_spent is greater than 100.

```sql
SELECT customer_id, SUM(amount) AS total_spent FROM payment
GROUP BY customer_id
HAVING total_spent > 100;
```
```text
ERROR:  column "total_spent" does not exist
LINE 3: HAVING total_spent > 100;
               ^ 

SQL state: 42703
Character: 89
```

> [!ERROR]
> You get an error similar to the above one, this is because total_spent is only going to get exist at the very end of our output. Therefore you cannot use alias with an **WHERE** or **HAVING** clause for filtering. 

> You can use the column name or the function to use filter.

```sql
SELECT customer_id, SUM(amount) AS total_spent FROM payment
GROUP BY customer_id
HAVING SUM(amount) > 100;
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>total_spent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>114.70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>123.74</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>130.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>134.65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7</td>
      <td>130.72</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> We will be using a lot of **AS** clause in the upcoming **JOIN** statments as they will quite useful to assign aliases for clarification.

---

### 2. JOINs