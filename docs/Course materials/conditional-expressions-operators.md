## Creating Databases & Tables

In this section of the course we are going to be focusing on being able to conduct logical operations and functionality within our SQL code. We will learning about keywords:
	
- CASE
- COALESCE
- NULLIF
- CAST

We are also going to learn about some additional functionality which allows us to expand on the usefulness of pgAdmin:

- Views
- Import and Export Functionality

These keywords and functions will allow us to add logic to our commands and workflows in SQL.

---

### 1. CASE

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
      <td>True</td>
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
      <td>True</td>
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
      <td>True</td>
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
      <td>True</td>
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
      <td>True</td>
      <td>2006-02-14</td>
      <td>2013-05-26 14:49:45.738</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

> Make some categories using the general CASE statment based on customer_id using the following conditions:

- If customer_id is less than 100, then the category is 'Premium'
- If customer_id is between 100 and 200, then the category is 'Gold'
- Everything other than above is 'Silver'

```sql
SELECT 
    customer_id, 
    CASE
        WHEN (customer_id < 100) THEN 'Premium'
        WHEN (customer_id >= 100 AND customer_id < 200) THEN 'Gold'
        ELSE 'Silver'
    END AS category
FROM customer;
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>524</td>
      <td>Silver</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Premium</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Premium</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Premium</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Premium</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> The general CASE statement is the one with the most flexible as you can check all kinds of conditions.

In most cases, you will see the CASE statement used only for checking equality of values. In such cases, you can use the simpler CASE statement.

> Imagine that you are running a raffle, where you have 3 prizes to give away.

- The customer with customer_id 1 is the winner.

- The customer with customer_id 2 is the second place winner.

- The customer with the customer_id 3 is the third place winner.

- Others are all losers.

```sql
SELECT 
    customer_id,
    CASE customer_id
        WHEN 1 THEN 'Winner'
        WHEN 2 THEN 'Second Place'
        WHEN 3 THEN 'Third Place'
        ELSE 'Loser'
    END AS prize
FROM customer;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>prize</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>524</td>
      <td>Loser</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Winner</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Second Place</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Third Place</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Loser</td>
    </tr>
  </tbody>
</table>

> Explore the `film` table.

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

> Find out the count of rental_rate whose value is $ 0.99. You need to use CASE for this problem.

```sql
SELECT 
  SUM(
  CASE rental_rate
    WHEN 0.99 THEN 1
    ELSE 0 
  END
) FROM film; 
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sum</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>341</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> You might think that you could have gotten the same results with much simpler solution using GROUPBY, COUNT, WHERE and HAVING. But what if i wanted to do the same for different categories?? Like for $ 2.99 and $ 

> Add columns for other categories with the same problem.

```sql
SELECT 
  SUM(
  CASE rental_rate
    WHEN 0.99 THEN 1
    ELSE 0 
  END
  ) AS bargains,
  SUM(
  CASE rental_rate
    WHEN 2.99 THEN 1
    ELSE 0 
  END
  ) AS regular,
  SUM(
  CASE rental_rate
    WHEN 4.99 THEN 1
    ELSE 0 
  END
  ) AS premium
FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>bargains</th>
      <th>regular</th>
      <th>premium</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>341</td>
      <td>323</td>
      <td>336</td>
    </tr>
  </tbody>
</table>

---

### 2. CAST

> Display the string '5' as integer 5.

```sql
SELECT CAST('5' AS INTEGER);
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>int4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
    </tr>
  </tbody>
</table>

> Try casting the string 'five' to integer 5.
```sql
SELECT CAST('five' AS INTEGER);
```
```text
ERROR:  invalid input syntax for type integer: "five"
LINE 1: SELECT CAST('five' AS INTEGER);
                    ^ 

SQL state: 22P02
Character: 13
```

> Utilize the special CAST operator provided by postgresql.

```sql
SELECT '5'::INTEGER;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>int4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
    </tr>
  </tbody>
</table>

> [!NOTE] 
> [This CAST operator is specifically created for postgresql only. Therefore you can only use this operator when you are using postgresql.]

> Explore the `rental` table

```sql
SELECT * FROM rental;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rental_id</th>
      <th>rental_date</th>
      <th>inventory_id</th>
      <th>customer_id</th>
      <th>return_date</th>
      <th>staff_id</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>2005-05-24 22:54:33</td>
      <td>1525</td>
      <td>459</td>
      <td>2005-05-28 19:40:33</td>
      <td>1</td>
      <td>2006-02-16 02:30:53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>2005-05-24 23:03:39</td>
      <td>1711</td>
      <td>408</td>
      <td>2005-06-01 22:12:39</td>
      <td>1</td>
      <td>2006-02-16 02:30:53</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td>2005-05-24 23:04:41</td>
      <td>2452</td>
      <td>333</td>
      <td>2005-06-03 01:43:41</td>
      <td>2</td>
      <td>2006-02-16 02:30:53</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>2005-05-24 23:05:21</td>
      <td>2079</td>
      <td>222</td>
      <td>2005-06-02 04:33:21</td>
      <td>1</td>
      <td>2006-02-16 02:30:53</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>2005-05-24 23:08:07</td>
      <td>2792</td>
      <td>549</td>
      <td>2005-05-27 01:32:07</td>
      <td>1</td>
      <td>2006-02-16 02:30:53</td>
    </tr>
  </tbody>
</table>

> Find out the length or the number of digits present in each of the inventory_id.

```sql
SELECT CHAR_LENGTH(CAST(inventory_id AS VARCHAR)) AS inventory_id_len
FROM rental;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>inventory_id_len</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
    </tr>
  </tbody>
</table>

---

### 3. NULLIF

> Create a new database `testdb` and create a new table named `depts`  

- Create the new table

```sql
CREATE TABLE depts(
  first_name VARCHAR(50),
  department VARCHAR(50)
);
```
```text
CREATE TABLE

Query returned successfully in 48 msec.
```

- Insert the data

```sql
INSERT INTO depts (first_name, department) 
VALUES 
('Vinton', 'A'),
('Lauren', 'A'),
('Claire', 'B');
```
```text
INSERT 0 3

Query returned successfully in 43 msec.
```

> Explore the recently created `depts` table.

```sql
SELECT * FROM depts;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>first_name</th>
      <th>department</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Vinton</td>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Lauren</td>
      <td>A</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Claire</td>
      <td>B</td>
    </tr>
  </tbody>
</table>

> Calculate the ratio between depts A to B.

```sql
SELECT
SUM(CASE WHEN department = 'A' THEN 1 ELSE 0 END) / 
SUM(CASE WHEN department = 'B' THEN 1 ELSE 0 END) AS department_ratio
FROM depts;
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>department_ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
    </tr>
  </tbody>
</table>

> Delete the rows with the department 'B'.

```sql
DELETE FROM depts
WHERE department = 'B';
```
```text
DELETE 1

Query returned successfully in 52 msec.
```

> Verify the deletion of the rows.

```sql
SELECT * FROM depts;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>first_name</th>
      <th>department</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Vinton</td>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Lauren</td>
      <td>A</td>
    </tr>
  </tbody>
</table>

> Again, try to calculate the ratio between depts A to B.

```sql
SELECT
SUM(CASE WHEN department = 'A' THEN 1 ELSE 0 END) / 
SUM(CASE WHEN department = 'B' THEN 1 ELSE 0 END) AS department_ratio
FROM depts;
```
```text
ERROR:  division by zero 

SQL state: 22012
```

> [!NOTE]
> The above error makes sense as now we are dividing something by 0. You can use the NULLIF clause to handle this sort of error.

> Calculate the ratio between depts A to B using the NULLIF.

```sql
SELECT
SUM(CASE WHEN department = 'A' THEN 1 ELSE 0 END) / 
NULLIF(SUM(CASE WHEN department = 'B' THEN 1 ELSE 0 END), 0) AS department_ratio
FROM depts;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>department_ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>None</td>
    </tr>
  </tbody>
</table>

> [!NOTE] 
> This time the result is not an error as we arent trying to divide something by 0 but by NULL. We're essentially using the NULLIF clause as a check against returning 0.