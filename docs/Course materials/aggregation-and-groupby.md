##  Aggregate Functions & GROUP BY Statements 

This document contains all the sql **GROUP BY** statements and aggregate functions, we executed for this course using the postgresql and pgadmin from the dvdrental datbase.

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

### 1. Aggregate Functions

> View all the columns of `film` table.

```sql
SELECT * FROM film
LIMIT 3;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>film_id</th>
      <th>title</th>
      <th>description</th>
      <th>release_year</th>
      <th>language_id</th>
      <th>rental_duration</th>
      <th>rental_rate</th>
      <th>length</th>
      <th>replacement_cost</th>
      <th>rating</th>
      <th>last_update</th>
      <th>special_features</th>
      <th>fulltext</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>133</td>
      <td>Chamber Italian</td>
      <td>A Fateful Reflection of a Moose And a Husband ...</td>
      <td>2006</td>
      <td>1</td>
      <td>7</td>
      <td>4.99</td>
      <td>117</td>
      <td>14.99</td>
      <td>NC-17</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Trailers}</td>
      <td>'chamber':1 'fate':4 'husband':11 'italian':2 ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>384</td>
      <td>Grosse Wonderful</td>
      <td>A Epic Drama of a Cat And a Explorer who must ...</td>
      <td>2006</td>
      <td>1</td>
      <td>5</td>
      <td>4.99</td>
      <td>49</td>
      <td>19.99</td>
      <td>R</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{"Behind the Scenes"}</td>
      <td>'australia':18 'cat':8 'drama':5 'epic':4 'exp...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>Airport Pollock</td>
      <td>A Epic Tale of a Moose And a Girl who must Con...</td>
      <td>2006</td>
      <td>1</td>
      <td>6</td>
      <td>4.99</td>
      <td>54</td>
      <td>15.99</td>
      <td>R</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Trailers}</td>
      <td>'airport':1 'ancient':18 'confront':14 'epic':...</td>
    </tr>
  </tbody>
</table>

> View the minimum replacement_cost.

```sql
SELECT MIN(replacement_cost) FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MIN(replacement_cost)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9.99</td>
    </tr>
  </tbody>
</table>

> View the maximum replacement_cost.

```sql
SELECT MAX(replacement_cost) FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MAX(replacement_cost)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>29.99</td>
    </tr>
  </tbody>
</table>

> View the maximum replacement_cost and film_id.

```sql
SELECT MAX(replacement_cost), film_id FROM film;
```
```text
ERROR:  column "film.film_id" must appear in the GROUP BY clause or be used in an aggregate function
LINE 1: SELECT MAX(replacement_cost), film_id FROM film;
                                      ^ 

SQL state: 42803
Character: 31
```

> [!WARNING]
> An aggregate function returns a single value. In this case, the MAX() returns the maximum replacement_cost as single floating numeric value. Therefore, it doesnt make any sense to call another column with this.

> [!NOTE]
> To call another column you can use the **GROUP BY** statement.

> View the minimum and maximum replacement_cost.

```sql
SELECT MAX(replacement_cost), MIN(replacement_cost)
FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MAX(replacement_cost)</th>
      <th>MIN(replacement_cost)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>29.99</td>
      <td>9.99</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
>The above query works because both MIN() and MAX() returns a single value.

> View the number of rows in the `film` table.

```sql
SELECT COUNT(*)
FROM film;
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
      <td>1000</td>
    </tr>
  </tbody>
</table>

> View the mean/average replacement_cost.

```sql
SELECT AVG(replacement_cost) FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AVG(replacement_cost)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>19.9840000000000000</td>
    </tr>
  </tbody>
</table>

> [!IMPORTANT]
> ROUND() function does a matchematical call, that rounds a result which is in floating numberic value to a specified number of decimal places.

>  View the mean/average replacement_cost rounded upto 2 decimal places.

```sql
SELECT ROUND(AVG(replacement_cost), 2) FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ROUND(AVG(replacement_cost), 2)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>19.98</td>
    </tr>
  </tbody>
</table>

> View the total replacement_cost from the `film` table.

```sql
SELECT SUM(replacement_cost)
FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SUM(replacement_cost)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>19984.0</td>
    </tr>
  </tbody>
</table>

*Now that we have familiarize ourselves with some of the basic and important aggregation function, we can go head and start using them in conjuction with **GROUP BY** statements*

--- 

### 2. GROUP BY 

> Explore the `payment` table.

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

> Group the actual customer_id.

```sql
SELECT customer_id FROM payment 
GROUP BY customer_id;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>341</td>
    </tr>
    <tr>
      <th>1</th>
      <td>342</td>
    </tr>
    <tr>
      <th>2</th>
      <td>343</td>
    </tr>
    <tr>
      <th>3</th>
      <td>344</td>
    </tr>
    <tr>
      <th>4</th>
      <td>345</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> The above query is just returning the unique customer_id, which is equivalent to the result of sql query: **SELECT DISTINCT customer_id FROM payment;**. This is beacause we simply grouping the customer_id column without using any aggregation function.

> Find out which customer is spending the most money in total.

```sql
SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC;
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
      <td>148</td>
      <td>211.55</td>
    </tr>
    <tr>
      <th>1</th>
      <td>526</td>
      <td>208.58</td>
    </tr>
    <tr>
      <th>2</th>
      <td>178</td>
      <td>194.61</td>
    </tr>
    <tr>
      <th>3</th>
      <td>137</td>
      <td>191.62</td>
    </tr>
    <tr>
      <th>4</th>
      <td>144</td>
      <td>189.60</td>
    </tr>
  </tbody>
</table>

> Additionally, also find out how many transactions did each customer made.

```sql
SELECT customer_id, SUM(amount), COUNT(amount) FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>SUM(amount)</th>
      <th>COUNT(amount)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>148</td>
      <td>211.55</td>
      <td>45</td>
    </tr>
    <tr>
      <th>1</th>
      <td>526</td>
      <td>208.58</td>
      <td>42</td>
    </tr>
    <tr>
      <th>2</th>
      <td>178</td>
      <td>194.61</td>
      <td>39</td>
    </tr>
    <tr>
      <th>3</th>
      <td>137</td>
      <td>191.62</td>
      <td>38</td>
    </tr>
    <tr>
      <th>4</th>
      <td>144</td>
      <td>189.60</td>
      <td>40</td>
    </tr>
  </tbody>
</table>

> Find out the total amount spent per staff per customer.

```sql
SELECT 
  staff_id,
  customer_id,
  SUM(amount) 
FROM payment
GROUP BY staff_id, customer_id
ORDER BY staff_id;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>staff_id</th>
      <th>customer_id</th>
      <th>SUM(amount)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>60.85</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>55.86</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>59.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>4</td>
      <td>49.88</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>5</td>
      <td>63.86</td>
    </tr>
  </tbody>
</table>

> Find out how many transactions are being processed each day.

```sql
SELECT 
	DATE(payment_date), 
	SUM(amount)
FROM payment
GROUP BY DATE(payment_date)
ORDER BY DATE(payment_date);
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>DATE(payment_date)</th>
      <th>SUM(amount)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2007-02-14</td>
      <td>116.73</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2007-02-15</td>
      <td>1188.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2007-02-16</td>
      <td>1154.18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2007-02-17</td>
      <td>1188.17</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2007-02-18</td>
      <td>1275.98</td>
    </tr>
  </tbody>
</table>

> [!IMPORTANT]
> The **DATE()** function extracts only the day portion of the timestamp information. We need to do this beacause the timestamp column has values down to the sub seconds.

--- 

### 3. HAVING

> Explore the `payment` table.

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

> Try running the below query:

```sql
SELECT customer_id, SUM(amount) FROM payment
WHERE SUM(amount) > 100
GROUP BY customer_id;
```
```text
ERROR:  aggregate functions are not allowed in WHERE
LINE 2: WHERE SUM(amount) > 100
              ^ 
SQL state: 42803
Character: 52
```

> The above query will show you an error, because the SUM(amount) cannot happen until after the group by is called.

> Try running the below query:

```sql
SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
HAVING SUM(amount) > 100;
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

> [!IMPORTANT]
> **HAVING** is used to filter grouped results after the **GROUP BY** clause has been applied.

> Explore the `customer` table.

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

> Find number of customers per store. Only show the stores which have more than 300 customers.

```sql
SELECT store_id, COUNT(store_id) FROM customer
GROUP BY store_id
HAVING COUNT(store_id) > 300;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store_id</th>
      <th>COUNT(store_id)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>326</td>
    </tr>
  </tbody>
</table>

---

# <div align="center">Thank You for Going Through This Guide! 🙏✨</div>