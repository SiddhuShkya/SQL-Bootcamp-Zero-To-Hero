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

