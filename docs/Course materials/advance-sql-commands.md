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

