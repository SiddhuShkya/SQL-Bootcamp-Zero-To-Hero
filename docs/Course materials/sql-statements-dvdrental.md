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

#### 1.1 **SELECT** statement

> View all columns from `actor` table

```sql
SELECT * FROM actor;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>actor_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Penelope</td>
      <td>Guiness</td>
      <td>2013-05-26 14:47:57.62</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Nick</td>
      <td>Wahlberg</td>
      <td>2013-05-26 14:47:57.62</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Ed</td>
      <td>Chase</td>
      <td>2013-05-26 14:47:57.62</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Jennifer</td>
      <td>Davis</td>
      <td>2013-05-26 14:47:57.62</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Johnny</td>
      <td>Lollobrigida</td>
      <td>2013-05-26 14:47:57.62</td>
    </tr>
  </tbody>
</table>

> View only one column from `actor`

```sql
SELECT first_name FROM actor;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>first_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Penelope</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nick</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ed</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jennifer</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Johnny</td>
    </tr>
  </tbody>
</table>

> View first_name and last_name from `actor` table

```sql
SELECT first_name, last_name FROM actor;
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>first_name</th>
      <th>last_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Penelope</td>
      <td>Guiness</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nick</td>
      <td>Wahlberg</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ed</td>
      <td>Chase</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jennifer</td>
      <td>Davis</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Johnny</td>
      <td>Lollobrigida</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> The order of the column names matters in the query as it determines the order of columns in the result set. [SELECT last_name, first_name] will display last_name in the first column and first_name in the second column.

#### 1.2 **SELECT DISTINCT** statement

> View all columns from `film` table

```sql
SELECT * FROM film;
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
    <tr>
      <th>3</th>
      <td>98</td>
      <td>Bright Encounters</td>
      <td>A Fateful Yarn of a Lumberjack And a Feminist ...</td>
      <td>2006</td>
      <td>1</td>
      <td>4</td>
      <td>4.99</td>
      <td>73</td>
      <td>12.99</td>
      <td>PG-13</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Trailers}</td>
      <td>'boat':20 'bright':1 'conquer':14 'encount':2 ...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>Academy Dinosaur</td>
      <td>A Epic Drama of a Feminist And a Mad Scientist...</td>
      <td>2006</td>
      <td>1</td>
      <td>6</td>
      <td>0.99</td>
      <td>86</td>
      <td>20.99</td>
      <td>PG</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{"Deleted Scenes","Behind the Scenes"}</td>
      <td>'academi':1 'battl':15 'canadian':20 'dinosaur...</td>
    </tr>
  </tbody>
</table>

> View distinct/unique release_years from `film` table

```sql
SELECT DISTINCT release_year FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>release_year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2006</td>
    </tr>
  </tbody>
</table>

> You can also use parenthesis with DISTINCT

```sql
SELECT DISTINCT(release_year) FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>release_year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2006</td>
    </tr>
  </tbody>
</table>

> View distinct/unique rental_rate from `film` table

```sql
SELECT DISTINCT(rental_rate) FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rental_rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4.99</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.99</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.99</td>
    </tr>
  </tbody>
</table>

#### 1.3 **COUNT** statement

> View all columns from `payment` table

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

> View the number of rows present in `payment` table.

```sql
SELECT COUNT(*) FROM payment;
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
      <td>14596</td>
    </tr>
  </tbody>
</table>

- View the number of rows in the amount column

```sql
SELECT COUNT(amount) FROM payment;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>COUNT(amount)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>14596</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> Note that using COUNT(*) or COUNT(amount) gives us the same number of result which is number of rows (14596). This is because the number of rows of the same table are always the same.

> View the actual number of unique amount in the amount column.

```sql
SELECT COUNT(DISTINCT amount) FROM payment;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>COUNT(DISTINCT amount)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>19</td>
    </tr>
  </tbody>
</table>

#### 1.4 **SELECT** & **WHERE** statement

> View all columns from `customer` table.

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

> View the rows who has the first_name 'Jared'.

```sql
SELECT * FROM customer
WHERE first_name = 'Jared';
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
  </tbody>
</table>

> View all columns from `film` table.

```sql
SELECT * FROM film;
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
    <tr>
      <th>3</th>
      <td>98</td>
      <td>Bright Encounters</td>
      <td>A Fateful Yarn of a Lumberjack And a Feminist ...</td>
      <td>2006</td>
      <td>1</td>
      <td>4</td>
      <td>4.99</td>
      <td>73</td>
      <td>12.99</td>
      <td>PG-13</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Trailers}</td>
      <td>'boat':20 'bright':1 'conquer':14 'encount':2 ...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>Academy Dinosaur</td>
      <td>A Epic Drama of a Feminist And a Mad Scientist...</td>
      <td>2006</td>
      <td>1</td>
      <td>6</td>
      <td>0.99</td>
      <td>86</td>
      <td>20.99</td>
      <td>PG</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{"Deleted Scenes","Behind the Scenes"}</td>
      <td>'academi':1 'battl':15 'canadian':20 'dinosaur...</td>
    </tr>
  </tbody>
</table>

> View all the rows whose rental_rate is higher than 4$.

```sql
SELECT * FROM film
WHERE rental_rate > 4;
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
    <tr>
      <th>3</th>
      <td>98</td>
      <td>Bright Encounters</td>
      <td>A Fateful Yarn of a Lumberjack And a Feminist ...</td>
      <td>2006</td>
      <td>1</td>
      <td>4</td>
      <td>4.99</td>
      <td>73</td>
      <td>12.99</td>
      <td>PG-13</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Trailers}</td>
      <td>'boat':20 'bright':1 'conquer':14 'encount':2 ...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>Ace Goldfinger</td>
      <td>A Astounding Epistle of a Database Administrat...</td>
      <td>2006</td>
      <td>1</td>
      <td>3</td>
      <td>4.99</td>
      <td>48</td>
      <td>12.99</td>
      <td>G</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Trailers,"Deleted Scenes"}</td>
      <td>'ace':1 'administr':9 'ancient':19 'astound':4...</td>
    </tr>
  </tbody>
</table>

> View all the rows whose rental_rate is higher than 4$ and also whose replacement_cost is more or equal to 19.99$.

```sql
SELECT * FROM film
WHERE rental_rate > 4 AND replacement_cost >= 19.99;
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
      <th>1</th>
      <td>7</td>
      <td>Airplane Sierra</td>
      <td>A Touching Saga of a Hunter And a Butler who m...</td>
      <td>2006</td>
      <td>1</td>
      <td>6</td>
      <td>4.99</td>
      <td>62</td>
      <td>28.99</td>
      <td>PG-13</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Trailers,"Deleted Scenes"}</td>
      <td>'airplan':1 'boat':20 'butler':11,16 'discov':...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10</td>
      <td>Aladdin Calendar</td>
      <td>A Action-Packed Tale of a Man And a Lumberjack...</td>
      <td>2006</td>
      <td>1</td>
      <td>6</td>
      <td>4.99</td>
      <td>63</td>
      <td>24.99</td>
      <td>NC-17</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Trailers,"Deleted Scenes"}</td>
      <td>'action':5 'action-pack':4 'aladdin':1 'ancien...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13</td>
      <td>Ali Forever</td>
      <td>A Action-Packed Drama of a Dentist And a Croco...</td>
      <td>2006</td>
      <td>1</td>
      <td>4</td>
      <td>4.99</td>
      <td>150</td>
      <td>21.99</td>
      <td>PG</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{"Deleted Scenes","Behind the Scenes"}</td>
      <td>'action':5 'action-pack':4 'ali':1 'battl':16 ...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20</td>
      <td>Amelie Hellfighters</td>
      <td>A Boring Drama of a Woman And a Squirrel who m...</td>
      <td>2006</td>
      <td>1</td>
      <td>4</td>
      <td>4.99</td>
      <td>79</td>
      <td>23.99</td>
      <td>R</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Commentaries,"Deleted Scenes","Behind the Sce...</td>
      <td>'ameli':1 'baloon':19 'bore':4 'conquer':14 'd...</td>
    </tr>
  </tbody>
</table>

> View all the rows of title, rental_rate, replacement_cost and rating columns from the `film` table, such that rental_rate is greater than $4 and replacement_cost is greater or equal to $19.99 and also whose rating is 'R'.

```sql
SELECT 
  title, 
  rental_rate, 
  replacement_cost, 
  rating 
FROM film 
WHERE rental_rate > 4
  AND replacement_cost >= 19.99
  AND rating = 'R';
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>rental_rate</th>
      <th>replacement_cost</th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Grosse Wonderful</td>
      <td>4.99</td>
      <td>19.99</td>
      <td>R</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Amelie Hellfighters</td>
      <td>4.99</td>
      <td>23.99</td>
      <td>R</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Beast Hunchback</td>
      <td>4.99</td>
      <td>22.99</td>
      <td>R</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Brooklyn Desert</td>
      <td>4.99</td>
      <td>21.99</td>
      <td>R</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bubble Grosse</td>
      <td>4.99</td>
      <td>20.99</td>
      <td>R</td>
    </tr>
  </tbody>
</table>

> View the number of titles of the `flim` table who meets the above conditions.

```sql
SELECT COUNT(*)
FROM film 
WHERE rental_rate > 4
  AND replacement_cost >= 19.99
  AND rating = 'R';
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
      <td>34</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> You can also use COUNT(title) instead of COUNT(*), since it will return the same result.

> View the number of titles who has the rating 'R' or 'PG-13' from the `film` table.

```sql
SELECT COUNT(title)
FROM film
WHERE rating = 'R' OR rating = 'PG-13';
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>COUNT(title)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>418</td>
    </tr>
  </tbody>
</table>

> View all columns from the `film` table whose rating is not 'R';

```sql
SELECT * FROM film
WHERE rating != 'R';
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
      <td>98</td>
      <td>Bright Encounters</td>
      <td>A Fateful Yarn of a Lumberjack And a Feminist ...</td>
      <td>2006</td>
      <td>1</td>
      <td>4</td>
      <td>4.99</td>
      <td>73</td>
      <td>12.99</td>
      <td>PG-13</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Trailers}</td>
      <td>'boat':20 'bright':1 'conquer':14 'encount':2 ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Academy Dinosaur</td>
      <td>A Epic Drama of a Feminist And a Mad Scientist...</td>
      <td>2006</td>
      <td>1</td>
      <td>6</td>
      <td>0.99</td>
      <td>86</td>
      <td>20.99</td>
      <td>PG</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{"Deleted Scenes","Behind the Scenes"}</td>
      <td>'academi':1 'battl':15 'canadian':20 'dinosaur...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>Ace Goldfinger</td>
      <td>A Astounding Epistle of a Database Administrat...</td>
      <td>2006</td>
      <td>1</td>
      <td>3</td>
      <td>4.99</td>
      <td>48</td>
      <td>12.99</td>
      <td>G</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Trailers,"Deleted Scenes"}</td>
      <td>'ace':1 'administr':9 'ancient':19 'astound':4...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>Adaptation Holes</td>
      <td>A Astounding Reflection of a Lumberjack And a ...</td>
      <td>2006</td>
      <td>1</td>
      <td>7</td>
      <td>2.99</td>
      <td>50</td>
      <td>18.99</td>
      <td>NC-17</td>
      <td>2013-05-26 14:50:58.951</td>
      <td>{Trailers,"Deleted Scenes"}</td>
      <td>'adapt':1 'astound':4 'baloon':19 'car':11 'fa...</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> You can also use the `<>` operator instead of `!=` as both of them behave the same way. 

#### 1.5 **ORDER BY** statement