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

- View all columns from `actor` table

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

> Returns all the information from the `actor` table

- View only one column from `actor`

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

> Returns only the first_name column from the `actor` table

- View first_name and last_name from `actor` table

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

> Returns first_name and last_name from `actor` table

> [!NOTE]
> The order of the column names matters in the query as it determines the order of columns in the result set. [SELECT last_name, first_name] will display last_name in the first column and first_name in the second column.

#### 1.2 **SELECT DISTINCT** statement

- View all columns from `film` table

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

> Returns all the information from the `film` table

- View distinct/unique release_years from `film` table

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

> Returns all the unique/distinct release_year present in the `film` table

- You can also use parenthesis with DISTINCT

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

> The result will be same with or without parenthesis.

- View distinct/unique rental_rate from `film` table

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

> Returns all the unique/distinct rental_rate present in the `film` table

#### 1.3 **SELECT WHERE** statement