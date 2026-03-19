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

### 1. **SELECT** statement

> View all columns from `actor` table

```postgresql
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

```postgresql
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

```postgresql
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

### 2. **SELECT DISTINCT** statement

> View all columns from `film` table

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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

### 3. **COUNT** statement

> View all columns from `payment` table

```postgresql
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

```postgresql
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

> View the number of rows in the amount column

```postgresql
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

```postgresql
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

### 4. **SELECT** & **WHERE** statement

> View all columns from `customer` table.

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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

```postgresql
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

### 5. **ORDER BY** statement

> View all columns from `customer` table

```postgresql
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

> Order the `customer` table based on the first_name of the user, which would be an alphabetical order based on first_name in ascending order.

```postgresql
SELECT * FROM customer
ORDER BY first_name ASC;
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
      <td>375</td>
      <td>2</td>
      <td>Aaron</td>
      <td>Selby</td>
      <td>aaron.selby@sakilacustomer.org</td>
      <td>380</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>367</td>
      <td>1</td>
      <td>Adam</td>
      <td>Gooch</td>
      <td>adam.gooch@sakilacustomer.org</td>
      <td>372</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>525</td>
      <td>2</td>
      <td>Adrian</td>
      <td>Clary</td>
      <td>adrian.clary@sakilacustomer.org</td>
      <td>531</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>217</td>
      <td>2</td>
      <td>Agnes</td>
      <td>Bishop</td>
      <td>agnes.bishop@sakilacustomer.org</td>
      <td>221</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>389</td>
      <td>1</td>
      <td>Alan</td>
      <td>Kahn</td>
      <td>alan.kahn@sakilacustomer.org</td>
      <td>394</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> For ordering in ascending order, you can either use the ASC keyword or leave it blank. 'SELECT * FROM customer ORDER BY first_name ASC' is equivalent to 'SELECT * FROM customer ORDER BY first_name'. 

> Run the same query above, but this time return the result in descending order based on first_name column.

```postgresql
SELECT * FROM customer
ORDER BY first_name DESC;
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
      <td>479</td>
      <td>1</td>
      <td>Zachary</td>
      <td>Hite</td>
      <td>zachary.hite@sakilacustomer.org</td>
      <td>484</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>174</td>
      <td>2</td>
      <td>Yvonne</td>
      <td>Watkins</td>
      <td>yvonne.watkins@sakilacustomer.org</td>
      <td>178</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>190</td>
      <td>2</td>
      <td>Yolanda</td>
      <td>Weaver</td>
      <td>yolanda.weaver@sakilacustomer.org</td>
      <td>194</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>212</td>
      <td>2</td>
      <td>Wilma</td>
      <td>Richards</td>
      <td>wilma.richards@sakilacustomer.org</td>
      <td>216</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>219</td>
      <td>2</td>
      <td>Willie</td>
      <td>Howell</td>
      <td>willie.howell@sakilacustomer.org</td>
      <td>223</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

> Order the `customer` table such that the query first orders the table based on store_id to get all the results per store, and then organize it by first_name column.

```postgresql
SELECT store_id, first_name, last_name FROM customer
ORDER BY store_id, first_name;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Adam</td>
      <td>Gooch</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Alan</td>
      <td>Kahn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Albert</td>
      <td>Crouse</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>Alice</td>
      <td>Stewart</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>Alicia</td>
      <td>Mills</td>
    </tr>
  </tbody>
</table>

> Run the same above query but this time order the rows based on 'store_id' in descending order to get results per store, followed by organzing it using the first_name column in ascending order.

```postgresql
SELECT first_name, last_name FROM customer
ORDER BY store_id DESC, first_name ASC;
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
      <td>Aaron</td>
      <td>Selby</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Adrian</td>
      <td>Clary</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agnes</td>
      <td>Bishop</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alberto</td>
      <td>Henning</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alex</td>
      <td>Gresham</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> Note that it is not necessary to specify the column which you are  using to order the table as long as the column exist in the original table. 

### 6. **LIMIT** statement

> View all columns from `payment` table

```postgresql
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

> View the top 3 most recent purchases in the payment table.

```postgresql
SELECT * FROM payment
ORDER BY payment_date DESC
LIMIT 3;
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
      <td>31917</td>
      <td>267</td>
      <td>2</td>
      <td>12066</td>
      <td>7.98</td>
      <td>2007-05-14 13:44:29.996577</td>
    </tr>
    <tr>
      <th>1</th>
      <td>31918</td>
      <td>267</td>
      <td>2</td>
      <td>13713</td>
      <td>0.00</td>
      <td>2007-05-14 13:44:29.996577</td>
    </tr>
    <tr>
      <th>2</th>
      <td>31919</td>
      <td>269</td>
      <td>1</td>
      <td>13025</td>
      <td>3.98</td>
      <td>2007-05-14 13:44:29.996577</td>
    </tr>
  </tbody>
</table>

### 7. **BETWEEN** statement

> View all the columns of the `payment` table

```postgresql
SELECT * FROM  payment
LIMIT 3;
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
  </tbody>
</table>

> View the rows, where the actual payments were done between $8 and $9.

```postgresql
SELECT * FROM  payment
WHERE amount BETWEEN 8 AND 9;
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
      <td>17517</td>
      <td>343</td>
      <td>1</td>
      <td>2980</td>
      <td>8.99</td>
      <td>2007-02-20 07:03:29.996577</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17529</td>
      <td>347</td>
      <td>2</td>
      <td>1711</td>
      <td>8.99</td>
      <td>2007-02-16 12:40:18.996577</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17532</td>
      <td>347</td>
      <td>1</td>
      <td>3092</td>
      <td>8.99</td>
      <td>2007-02-20 14:33:08.996577</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17535</td>
      <td>348</td>
      <td>1</td>
      <td>2041</td>
      <td>8.99</td>
      <td>2007-02-17 12:47:26.996577</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17540</td>
      <td>349</td>
      <td>1</td>
      <td>3067</td>
      <td>8.99</td>
      <td>2007-02-20 12:27:47.996577</td>
    </tr>
  </tbody>
</table>

> View the number of payments that satisfied the above condition.

```postgresql
SELECT COUNT(*) FROM  payment
WHERE amount BETWEEN 8 AND 9;
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
      <td>439</td>
    </tr>
  </tbody>
</table>

> View the number of payments that does not satify the above condition.

```postgresql
SELECT COUNT(*) FROM  payment
WHERE amount NOT BETWEEN 8 AND 9;
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
      <td>14157</td>
    </tr>
  </tbody>
</table>

> View all the payments that happened on the first half of feburary 2007.

```postgresql
SELECT * FROM payment
WHERE payment_date BETWEEN '2007-02-01' AND '2007-02-15';
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
      <td>17610</td>
      <td>368</td>
      <td>1</td>
      <td>1186</td>
      <td>0.99</td>
      <td>2007-02-14 23:25:11.996577</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17617</td>
      <td>370</td>
      <td>2</td>
      <td>1190</td>
      <td>6.99</td>
      <td>2007-02-14 23:33:58.996577</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17743</td>
      <td>402</td>
      <td>2</td>
      <td>1194</td>
      <td>4.99</td>
      <td>2007-02-14 23:53:34.996577</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17793</td>
      <td>416</td>
      <td>2</td>
      <td>1158</td>
      <td>2.99</td>
      <td>2007-02-14 21:21:59.996577</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17854</td>
      <td>432</td>
      <td>2</td>
      <td>1180</td>
      <td>5.99</td>
      <td>2007-02-14 23:07:27.996577</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> Note that when we are dealing with timestamp information which includes both the date and hour, minutes, etc., PostgreSQL has to decide whether a day starts at 0:00 hours or at 24:00 hours. In the `BETWEEN` operator, PostgreSQL interprets date literals without time components as midnight (00:00:00) of that date. This means `BETWEEN '2007-02-01' AND '2007-02-15'` is equivalent to `BETWEEN '2007-02-01 00:00:00' AND '2007-02-15 00:00:00'`, which **excludes** all timestamps after midnight on February 15th. To include the entire day of February 15th, you should use `BETWEEN '2007-02-01' AND '2007-02-15 23:59:59'` or better yet, `BETWEEN '2007-02-01' AND '2007-02-16'` (exclusive upper bound), or use `payment_date >= '2007-02-01' AND payment_date < '2007-02-16'`.

### 8. **IN** statement

> View all columns of `payment` table.

```postgresql
SELECT * FROM payment
LIMIT 3;
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
  </tbody>
</table>

> View the actual distinct values that are available in the amount column.

```postgresql
SELECT DISTINCT(amount) FROM payment
ORDER BY amount;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.99</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.98</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.99</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.99</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3.99</td>
    </tr>
    <tr>
      <th>7</th>
      <td>4.99</td>
    </tr>
    <tr>
      <th>8</th>
      <td>5.98</td>
    </tr>
    <tr>
      <th>9</th>
      <td>5.99</td>
    </tr>
    <tr>
      <th>10</th>
      <td>6.99</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7.98</td>
    </tr>
    <tr>
      <th>12</th>
      <td>7.99</td>
    </tr>
    <tr>
      <th>13</th>
      <td>8.97</td>
    </tr>
    <tr>
      <th>14</th>
      <td>8.99</td>
    </tr>
    <tr>
      <th>15</th>
      <td>9.98</td>
    </tr>
    <tr>
      <th>16</th>
      <td>9.99</td>
    </tr>
    <tr>
      <th>17</th>
      <td>10.99</td>
    </tr>
    <tr>
      <th>18</th>
      <td>11.99</td>
    </tr>
  </tbody>
</table>

> View all the information of the `payment` table where amount happens to be $0.99, $1.98 and $1.98.

```postgresql
SELECT * FROM payment
WHERE amount IN (0.99, 1.98, 1.99)
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
      <td>17504</td>
      <td>341</td>
      <td>1</td>
      <td>1778</td>
      <td>1.99</td>
      <td>2007-02-16 17:23:14.996577</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17514</td>
      <td>343</td>
      <td>2</td>
      <td>1879</td>
      <td>0.99</td>
      <td>2007-02-17 01:26:00.996577</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17515</td>
      <td>343</td>
      <td>2</td>
      <td>1922</td>
      <td>0.99</td>
      <td>2007-02-17 04:32:51.996577</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17518</td>
      <td>343</td>
      <td>1</td>
      <td>3407</td>
      <td>0.99</td>
      <td>2007-02-21 14:42:28.996577</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17521</td>
      <td>344</td>
      <td>1</td>
      <td>1731</td>
      <td>0.99</td>
      <td>2007-02-16 14:00:38.996577</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> Notice that im not using quotes for the amount values. This is because the amount column is of numeric data type.

> View the number of payments that has the amount which satisfies the above condition.

```postgresql
SELECT COUNT(*) FROM payment
WHERE amount IN (0.99, 1.98, 1.99)
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
      <td>3301</td>
    </tr>
  </tbody>
</table>

> Similarly, view the number of payments that doesnt have the amount which satisfies the above condition.

```postgresql
SELECT COUNT(*) FROM payment
WHERE amount NOT IN (0.99, 1.98, 1.99)
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
      <td>11295</td>
    </tr>
  </tbody>
</table>

> View all the columns of the `customer` table.

```postgresql
SELECT * FROM customer
LIMIT 3;
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
  </tbody>
</table>

> View all the information from the `customer` table whose first_name is either 'John', 'Jake' or 'Julie'.

```postgresql
SELECT * FROM customer
WHERE first_name IN ('John', 'Jake', 'Julie');
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
      <td>52</td>
      <td>1</td>
      <td>Julie</td>
      <td>Sanchez</td>
      <td>julie.sanchez@sakilacustomer.org</td>
      <td>56</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>300</td>
      <td>1</td>
      <td>John</td>
      <td>Farnsworth</td>
      <td>john.farnsworth@sakilacustomer.org</td>
      <td>305</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

*The output only shows 'Julie' & 'John' because 'Jake' doesnt exists in the `customer` table*

### 9. **LIKE & ILIKE** statement

> View all the columns of the `customer` table.

```postgresql
SELECT * FROM customer
LIMIT 3;
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
  </tbody>
</table>

> Find out how many customers names that starts with an 'J'.

```postgresql
SELECT COUNT(*) FROM customer
WHERE first_name LIKE 'J%';
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
      <td>65</td>
    </tr>
  </tbody>
</table>

> View all the information of `customer` that has first_name that starts with an 'J' and also whose last_name starts with an 'S'.

```postgresql
SELECT * FROM customer
WHERE first_name LIKE 'J%' AND last_name LIKE 'S%';
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
      <td>52</td>
      <td>1</td>
      <td>Julie</td>
      <td>Sanchez</td>
      <td>julie.sanchez@sakilacustomer.org</td>
      <td>56</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>328</td>
      <td>2</td>
      <td>Jeffrey</td>
      <td>Spear</td>
      <td>jeffrey.spear@sakilacustomer.org</td>
      <td>333</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>353</td>
      <td>1</td>
      <td>Jonathan</td>
      <td>Scarborough</td>
      <td>jonathan.scarborough@sakilacustomer.org</td>
      <td>358</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>387</td>
      <td>2</td>
      <td>Jesse</td>
      <td>Schilling</td>
      <td>jesse.schilling@sakilacustomer.org</td>
      <td>392</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>397</td>
      <td>1</td>
      <td>Jimmy</td>
      <td>Schrader</td>
      <td>jimmy.schrader@sakilacustomer.org</td>
      <td>402</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

> [!IMPORTANT]
> In the above statements i used capital 'J' and 'S' because i was using *LIKE*. If i were to use lowercase 'j' and 's', the result would be different. This is because *LIKE* is case sensitive. If you dont want to know the case of the letter in account, then you can also use *ILIKE*.

> View all the information of `customer` that has first_name that starts with an 'J' and also whose last_name starts with an 's' using **ILIKE**.

```postgresql
SELECT * FROM customer
WHERE first_name ILIKE 'j%' AND last_name ILIKE 's%';
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
      <td>52</td>
      <td>1</td>
      <td>Julie</td>
      <td>Sanchez</td>
      <td>julie.sanchez@sakilacustomer.org</td>
      <td>56</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>328</td>
      <td>2</td>
      <td>Jeffrey</td>
      <td>Spear</td>
      <td>jeffrey.spear@sakilacustomer.org</td>
      <td>333</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>353</td>
      <td>1</td>
      <td>Jonathan</td>
      <td>Scarborough</td>
      <td>jonathan.scarborough@sakilacustomer.org</td>
      <td>358</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>387</td>
      <td>2</td>
      <td>Jesse</td>
      <td>Schilling</td>
      <td>jesse.schilling@sakilacustomer.org</td>
      <td>392</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>397</td>
      <td>1</td>
      <td>Jimmy</td>
      <td>Schrader</td>
      <td>jimmy.schrader@sakilacustomer.org</td>
      <td>402</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

> View all the information of `customer` that has 'er' somewhere in their first_name and also in last_name.

```postgresql
SELECT * FROM customer
WHERE first_name LIKE '%er%' AND last_name LIKE '%er%';
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
      <td>54</td>
      <td>1</td>
      <td>Teresa</td>
      <td>Rogers</td>
      <td>teresa.rogers@sakilacustomer.org</td>
      <td>58</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>61</td>
      <td>2</td>
      <td>Katherine</td>
      <td>Rivera</td>
      <td>katherine.rivera@sakilacustomer.org</td>
      <td>65</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>156</td>
      <td>1</td>
      <td>Bertha</td>
      <td>Ferguson</td>
      <td>bertha.ferguson@sakilacustomer.org</td>
      <td>160</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>161</td>
      <td>1</td>
      <td>Geraldine</td>
      <td>Perkins</td>
      <td>geraldine.perkins@sakilacustomer.org</td>
      <td>165</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>185</td>
      <td>1</td>
      <td>Roberta</td>
      <td>Harper</td>
      <td>roberta.harper@sakilacustomer.org</td>
      <td>189</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> Notice, in the last row 'Harper', the 'er' is at the end. Therefore, % (sequence of characters) can also be nothing and that 'er' doesnt have to be between any other letters.

> View all the information of the `customer` table where the first letter matches exactly one character, followed exactly by 'her'.

```postgresql
SELECT * FROM customer
WHERE first_name LIKE '_her%';
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
      <td>59</td>
      <td>1</td>
      <td>Cheryl</td>
      <td>Murphy</td>
      <td>cheryl.murphy@sakilacustomer.org</td>
      <td>63</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>72</td>
      <td>2</td>
      <td>Theresa</td>
      <td>Watson</td>
      <td>theresa.watson@sakilacustomer.org</td>
      <td>76</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>119</td>
      <td>1</td>
      <td>Sherry</td>
      <td>Marshall</td>
      <td>sherry.marshall@sakilacustomer.org</td>
      <td>123</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>297</td>
      <td>1</td>
      <td>Sherri</td>
      <td>Rhodes</td>
      <td>sherri.rhodes@sakilacustomer.org</td>
      <td>302</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

> View all the information of `customer` whose first_name starts with an 'A' and also order the result in ascending order based on first_name.

```postgresql
SELECT * FROM customer
WHERE first_name LIKE 'A%'
ORDER BY first_name;
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
      <td>375</td>
      <td>2</td>
      <td>Aaron</td>
      <td>Selby</td>
      <td>aaron.selby@sakilacustomer.org</td>
      <td>380</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>367</td>
      <td>1</td>
      <td>Adam</td>
      <td>Gooch</td>
      <td>adam.gooch@sakilacustomer.org</td>
      <td>372</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>525</td>
      <td>2</td>
      <td>Adrian</td>
      <td>Clary</td>
      <td>adrian.clary@sakilacustomer.org</td>
      <td>531</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>217</td>
      <td>2</td>
      <td>Agnes</td>
      <td>Bishop</td>
      <td>agnes.bishop@sakilacustomer.org</td>
      <td>221</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>389</td>
      <td>1</td>
      <td>Alan</td>
      <td>Kahn</td>
      <td>alan.kahn@sakilacustomer.org</td>
      <td>394</td>
      <td>1</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

---

# <div align="center">Thank You for Going Through This Guide! 🙏✨</div>