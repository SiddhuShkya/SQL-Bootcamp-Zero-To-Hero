##  Advance SQL Commands

This guide covers a set of powerful SQL techniques that go beyond the basics, helping you write more expressive, efficient, and flexible queries. What's covered:

1. Timestamps & Extract
2. Math Functions
3. String Functions
4. Sub-query
5. Self-Join

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

### 1. Timestamps & Extract

> Display all current configuration parameters and their values for the PostgreSQL session.

```sql
SHOW ALL;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>setting</th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>allow_in_place_tablespaces</td>
      <td>off</td>
      <td>Allows tablespaces directly inside pg_tblspc, ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>allow_system_table_mods</td>
      <td>off</td>
      <td>Allows modifications of the structure of syste...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>application_name</td>
      <td>pgAdmin 4 - CONN:6155437</td>
      <td>Sets the application name to be reported in st...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>archive_cleanup_command</td>
      <td>NaN</td>
      <td>Sets the shell command that will be executed a...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>archive_command</td>
      <td>(disabled)</td>
      <td>Sets the shell command that will be called to ...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>archive_library</td>
      <td>NaN</td>
      <td>Sets the library that will be called to archiv...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>archive_mode</td>
      <td>off</td>
      <td>Allows archiving of WAL files using archive_co...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>archive_timeout</td>
      <td>0</td>
      <td>Sets the amount of time to wait before forcing...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>array_nulls</td>
      <td>on</td>
      <td>Enable input of NULL elements in arrays.</td>
    </tr>
    <tr>
      <th>9</th>
      <td>authentication_timeout</td>
      <td>1min</td>
      <td>Sets the maximum allowed time to complete clie...</td>
    </tr>
  </tbody>
</table>

> Display only the current timezone setting for the session — the timezone PostgreSQL uses when interpreting or displaying timestamp values.

```sql
SHOW TIMEZONE;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TimeZone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Asia/Kathmandu</td>
    </tr>
  </tbody>
</table>

> Display the current timestamp information.

```sql
SELECT NOW();
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>now</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2026-03-06 00:23:46.347489+05:45</td>
    </tr>
  </tbody>
</table>

> Change the timezone format to string for readability.

```sql
SELECT TIMEOFDAY();
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>timeofday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fri Mar 06 00:27:23.315219 2026 +0545</td>
    </tr>
  </tbody>
</table>

> Display only the current time.

```sql
SELECT CURRENT_TIME;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>current_time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00:29:58.898873+05:45</td>
    </tr>
  </tbody>
</table>

> Display only the current date.

```sql
SELECT CURRENT_DATE;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>current_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2026-03-06</td>
    </tr>
  </tbody>
</table>

> View the `payment` table.

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

> Extract **YEAR** FROM payment_date.

```sql
SELECT EXTRACT(YEAR FROM payment_date) AS my_year
FROM payment;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>my_year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2007</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2007</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2007</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2007</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2007</td>
    </tr>
  </tbody>
</table>

> Extract **MONTH** FROM payment_date.

```sql
SELECT EXTRACT(MONTH FROM payment_date) AS pay_month
FROM payment;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pay_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.0</td>
    </tr>
  </tbody>
</table>

> Extract **QUARTER** of the month FROM payment_date.

```sql
SELECT EXTRACT(QUARTER FROM payment_date) AS pay_month
FROM payment;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pay_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.0</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> A quarter represents a 3-month period in a year.

| Quarter | Months    |
| ------- | --------- |
| 1       | Jan – Mar |
| 2       | Apr – Jun |
| 3       | Jul – Sep |
| 4       | Oct – Dec |

> Check how old the timestamp date was in regards to the current moment/date.

```sql
SELECT AGE(payment_date) 
FROM payment;
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6953 days 01:34:13.003423</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6952 days 06:36:45.003423</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6952 days 01:18:14.003423</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6949 days 04:20:03.003423</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6948 days 06:28:11.003423</td>
    </tr>
  </tbody>
</table>

> Convert the timestamp datatype of the payment_date column.

Source: [Functions Formatting](https://www.postgresql.org/docs/15/functions-formatting.html)

```sql
SELECT TO_CHAR(payment_date, 'MONTH -> YYYY')
FROM payment;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>to_char</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>FEBRUARY&nbsp;&nbsp;-&gt; 2007</td>
    </tr>
    <tr>
      <th>1</th>
      <td>FEBRUARY&nbsp;&nbsp;-&gt; 2007</td>
    </tr>
    <tr>
      <th>2</th>
      <td>FEBRUARY&nbsp;&nbsp;-&gt; 2007</td>
    </tr>
    <tr>
      <th>3</th>
      <td>FEBRUARY&nbsp;&nbsp;-&gt; 2007</td>
    </tr>
    <tr>
      <th>4</th>
      <td>FEBRUARY&nbsp;&nbsp;-&gt; 2007</td>
    </tr>
  </tbody>
</table>

```sql
SELECT TO_CHAR(payment_date, 'mon/dd/YYYY')
FROM payment;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>to_char</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>feb/15/2007</td>
    </tr>
    <tr>
      <th>1</th>
      <td>feb/16/2007</td>
    </tr>
    <tr>
      <th>2</th>
      <td>feb/16/2007</td>
    </tr>
    <tr>
      <th>3</th>
      <td>feb/19/2007</td>
    </tr>
    <tr>
      <th>4</th>
      <td>feb/20/2007</td>
    </tr>
  </tbody>
</table>

```sql
SELECT TO_CHAR(payment_date, 'MM/dd/YYYY')
FROM payment;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>to_char</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>02/15/2007</td>
    </tr>
    <tr>
      <th>1</th>
      <td>02/16/2007</td>
    </tr>
    <tr>
      <th>2</th>
      <td>02/16/2007</td>
    </tr>
    <tr>
      <th>3</th>
      <td>02/19/2007</td>
    </tr>
    <tr>
      <th>4</th>
      <td>02/20/2007</td>
    </tr>
  </tbody>
</table>

```sql
SELECT TO_CHAR(payment_date, 'YYYY-MM-DD')
FROM payment;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>to_char</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2007-02-15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2007-02-16</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2007-02-16</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2007-02-19</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2007-02-20</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> This is a note in regards to the next lecture, we've gotten a lot of questions of why TO_CHAR "doesn't work" for one of the assessment questions. It actually does work, but you need to realize certain codes are "blank padded to 9 characters", which means instead of returning 'Monday' it returns 'Monday   ' with extra spaces to fill up at least 9 spaces.

---

### 2. Mathematical Functions & Operators

Source : [Mathematical Functionsn & Operators](https://www.postgresql.org/docs/current/functions-math.html)

> View the `film` table.

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
      <td>[Trailers]</td>
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
      <td>[Behind the Scenes]</td>
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
      <td>[Trailers]</td>
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
      <td>[Trailers]</td>
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
      <td>[Deleted Scenes, Behind the Scenes]</td>
      <td>'academi':1 'battl':15 'canadian':20 'dinosaur...</td>
    </tr>
  </tbody>
</table>

> Find out what percentage of the replacement_cost is a rental rate.

```sql
SELECT ROUND(rental_rate/replacement_cost, 2) * 100 AS percent_cost
FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>percent_cost</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>33.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>25.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>31.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>38.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.00</td>
    </tr>
  </tbody>
</table>

> Put some small deposits down of 10% of the replacement_cost.

```sql
SELECT 0.1 * replacement_cost AS deposit
FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>deposit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.499</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.999</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.599</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.299</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.099</td>
    </tr>
  </tbody>
</table>