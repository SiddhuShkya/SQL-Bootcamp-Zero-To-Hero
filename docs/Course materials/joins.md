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

> [!IMPORTANT]
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

### 2. INNER JOIN

> View `customer` and `payment` table.

```sql
SELECT * FROM 
customer;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>activebool</th>
      <th>create_date</th>
      <th>last_update</th>
      <th>active</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>524</td>
      <td>1</td>
      <td>Jared</td>
      <td>Ely</td>
      <td>jared.ely@sakilacustomer.org</td>
      <td>530</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Mary</td>
      <td>Smith</td>
      <td>mary.smith@sakilacustomer.org</td>
      <td>5</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>1</td>
      <td>Patricia</td>
      <td>Johnson</td>
      <td>patricia.johnson@sakilacustomer.org</td>
      <td>6</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1</td>
      <td>Linda</td>
      <td>Williams</td>
      <td>linda.williams@sakilacustomer.org</td>
      <td>7</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2</td>
      <td>Barbara</td>
      <td>Jones</td>
      <td>barbara.jones@sakilacustomer.org</td>
      <td>8</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

```sql
SELECT * FROM 
payment;
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

> View the customer email associated with specific payment.

```sql
SELECT * FROM payment
INNER JOIN customer
ON payment.customer_id = customer.customer_id;
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
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>activebool</th>
      <th>create_date</th>
      <th>last_update</th>
      <th>active</th>
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
      <td>341</td>
      <td>1</td>
      <td>Peter</td>
      <td>Menard</td>
      <td>peter.menard@sakilacustomer.org</td>
      <td>346</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17504</td>
      <td>341</td>
      <td>1</td>
      <td>1778</td>
      <td>1.99</td>
      <td>2007-02-16 17:23:14.996577</td>
      <td>341</td>
      <td>1</td>
      <td>Peter</td>
      <td>Menard</td>
      <td>peter.menard@sakilacustomer.org</td>
      <td>346</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17505</td>
      <td>341</td>
      <td>1</td>
      <td>1849</td>
      <td>7.99</td>
      <td>2007-02-16 22:41:45.996577</td>
      <td>341</td>
      <td>1</td>
      <td>Peter</td>
      <td>Menard</td>
      <td>peter.menard@sakilacustomer.org</td>
      <td>346</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17506</td>
      <td>341</td>
      <td>2</td>
      <td>2829</td>
      <td>2.99</td>
      <td>2007-02-19 19:39:56.996577</td>
      <td>341</td>
      <td>1</td>
      <td>Peter</td>
      <td>Menard</td>
      <td>peter.menard@sakilacustomer.org</td>
      <td>346</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17507</td>
      <td>341</td>
      <td>2</td>
      <td>3130</td>
      <td>7.99</td>
      <td>2007-02-20 17:31:48.996577</td>
      <td>341</td>
      <td>1</td>
      <td>Peter</td>
      <td>Menard</td>
      <td>peter.menard@sakilacustomer.org</td>
      <td>346</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

> [!IMPORTANT]
> Since, we are using **INNER JOIN** it will return only the records that exists in both `payment` and `customer` table. Therefore, the result won't have the record of a customer who hasn't made any sort of payment.

> View only the specific columns: payment_id, customer_id, first_name

```sql
SELECT payment_id, payment.customer_id, first_name
FROM payment
INNER JOIN customer
ON payment.customer_id = customer.customer_id;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>payment_id</th>
      <th>customer_id</th>
      <th>first_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>17503</td>
      <td>341</td>
      <td>Peter</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17504</td>
      <td>341</td>
      <td>Peter</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17505</td>
      <td>341</td>
      <td>Peter</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17506</td>
      <td>341</td>
      <td>Peter</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17507</td>
      <td>341</td>
      <td>Peter</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> The payment_id is unique to `payment` table and the first_name is unique to `customer` table. However the customer_id exists in both table, so we need to clarify which customer_id we are refering to (**payment.customer_id**: takes customer_id of `payment` table). You can also clarify the payment_id and first_name using **payment.payment_id** and **customer.first_name** respectively. 

---

### 3. OUTER JOIN

There are few different types of OUTER JOINs, which allows us to deal with values only present in one of the tables being joined. They are much more complex JOINs than the simpler INNER JOINs.

*There are mainly 3 types of outer joins:*

#### 3.1 FULL OUTER JOIN

> View `customer` and `payment` table.

```sql
SELECT * FROM customer;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>activebool</th>
      <th>create_date</th>
      <th>last_update</th>
      <th>active</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>524</td>
      <td>1</td>
      <td>Jared</td>
      <td>Ely</td>
      <td>jared.ely@sakilacustomer.org</td>
      <td>530</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Mary</td>
      <td>Smith</td>
      <td>mary.smith@sakilacustomer.org</td>
      <td>5</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>1</td>
      <td>Patricia</td>
      <td>Johnson</td>
      <td>patricia.johnson@sakilacustomer.org</td>
      <td>6</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1</td>
      <td>Linda</td>
      <td>Williams</td>
      <td>linda.williams@sakilacustomer.org</td>
      <td>7</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2</td>
      <td>Barbara</td>
      <td>Jones</td>
      <td>barbara.jones@sakilacustomer.org</td>
      <td>8</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

```sql
SELECT * FROM payment;
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

> View all the payments that are associated with the current customer and all the customers that are associated with an historical payment.

```sql
SELECT * FROM customer
FULL OUTER JOIN payment
  ON customer.customer_id = payment.customer_id;
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>activebool</th>
      <th>create_date</th>
      <th>last_update</th>
      <th>active</th>
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
      <td>524</td>
      <td>1</td>
      <td>Jared</td>
      <td>Ely</td>
      <td>jared.ely@sakilacustomer.org</td>
      <td>530</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
      <td>18202</td>
      <td>524</td>
      <td>1</td>
      <td>1306</td>
      <td>1.99</td>
      <td>2007-02-15 08:27:50.996577</td>
    </tr>
    <tr>
      <th>1</th>
      <td>524</td>
      <td>1</td>
      <td>Jared</td>
      <td>Ely</td>
      <td>jared.ely@sakilacustomer.org</td>
      <td>530</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
      <td>18203</td>
      <td>524</td>
      <td>2</td>
      <td>1651</td>
      <td>4.99</td>
      <td>2007-02-16 07:53:04.996577</td>
    </tr>
    <tr>
      <th>2</th>
      <td>524</td>
      <td>1</td>
      <td>Jared</td>
      <td>Ely</td>
      <td>jared.ely@sakilacustomer.org</td>
      <td>530</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
      <td>18204</td>
      <td>524</td>
      <td>2</td>
      <td>3454</td>
      <td>2.99</td>
      <td>2007-02-21 19:40:39.996577</td>
    </tr>
    <tr>
      <th>3</th>
      <td>524</td>
      <td>1</td>
      <td>Jared</td>
      <td>Ely</td>
      <td>jared.ely@sakilacustomer.org</td>
      <td>530</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
      <td>21950</td>
      <td>524</td>
      <td>2</td>
      <td>13626</td>
      <td>2.99</td>
      <td>2007-03-20 05:23:50.996577</td>
    </tr>
    <tr>
      <th>4</th>
      <td>524</td>
      <td>1</td>
      <td>Jared</td>
      <td>Ely</td>
      <td>jared.ely@sakilacustomer.org</td>
      <td>530</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
      <td>21951</td>
      <td>524</td>
      <td>2</td>
      <td>14046</td>
      <td>4.99</td>
      <td>2007-03-20 20:21:47.996577</td>
    </tr>
  </tbody>
</table>

*The query simply returns all the rows from payment and customer table joined together*

> Filter the above result so that the information is unique to payment, not associative customer or unique to customer.

```sql
SELECT * FROM customer
FULL OUTER JOIN payment
  ON customer.customer_id = payment.customer_id
WHERE customer.customer_id IS NULL
OR payment.payment_id IS NULL;
```
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>activebool</th>
      <th>create_date</th>
      <th>last_update</th>
      <th>active</th>
      <th>payment_id</th>
      <th>customer_id</th>
      <th>staff_id</th>
      <th>rental_id</th>
      <th>amount</th>
      <th>payment_date</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

> [!NOTE]
> The empty rows states that, we dont have any payment information not associated with some customer and we also, dont have any customer information, who has never made a payment.

> Try verifying the result using the **DISTINCT** keyword. *Hint: The unique number of customer_id in the payment table must match the number of rows in the customer table*

```sql
SELECT COUNT(DISTINCT customer_id) FROM payment;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>COUNT(DISTINCT customer_id)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>599</td>
    </tr>
  </tbody>
</table>

```sql
SELECT COUNT(*) FROM customer;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>COUNT(*)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>599</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> Technically, the above process doesn't fully answer the previous privacy compliance, because there could could be different ID numbers in different tables. Therefore, it doesnt fully answer the quetion.

#### 3.2 LEFT OUTER JOIN