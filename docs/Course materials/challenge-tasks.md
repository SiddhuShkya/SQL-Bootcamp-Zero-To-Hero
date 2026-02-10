## Challenge Tasks

This document will contain all the challenges that were presented to me for a better learning experience. Challenges are structured in the below manners:

- Business Situation
- Challenge Question
- Expected Answer
- Hints
- Solution

---

### 1. SELECT 

> `Business Situation` : We want to send out promotional email to our existing customers!

> `Challenge` : Use a SELECT statement to grab the first and last names of every cutsomers and their email addresses.

> `Expected Answer`: 

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jared</td>
      <td>Ely</td>
      <td>jared.ely@sakilacustomer.org</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mary</td>
      <td>Smith</td>
      <td>mary.smith@sakilacustomer.org</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Patricia</td>
      <td>Johnson</td>
      <td>patricia.johnson@sakilacustomer.org</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Linda</td>
      <td>Williams</td>
      <td>linda.williams@sakilacustomer.org</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Barbara</td>
      <td>Jones</td>
      <td>barbara.jones@sakilacustomer.org</td>
    </tr>
  </tbody>
</table>

> `Hints`:
  - Use the `customer` table
  - You can use the table drop-down to view what columns are available
  - You could also use SELECT * FROM `customer` to see all then columns

> `Solutions`:

- View all columns from `customer` table

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

- View first_name, last_name, email from `customer`

```sql
SELECT first_name, last_name, email FROM customer;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jared</td>
      <td>Ely</td>
      <td>jared.ely@sakilacustomer.org</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mary</td>
      <td>Smith</td>
      <td>mary.smith@sakilacustomer.org</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Patricia</td>
      <td>Johnson</td>
      <td>patricia.johnson@sakilacustomer.org</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Linda</td>
      <td>Williams</td>
      <td>linda.williams@sakilacustomer.org</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Barbara</td>
      <td>Jones</td>
      <td>barbara.jones@sakilacustomer.org</td>
    </tr>
  </tbody>
</table>

---

### 2. SELECT DISTINCT

> `Business Situation`: 
- An Australian visitor isn't familiar with MPAA movie ratings (e.g. PG, PG-13, R, etc)
- We want to know the types of ratings, we have in our database.
- What ratings do we have available ? 

> `Challenge`: Use what you've learned about SELECT DISTINCT to retrieve the distinct rating types our films could have in our database.

> `Expected Answer`: 
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NC-17</td>
    </tr>
    <tr>
      <th>1</th>
      <td>R</td>
    </tr>
    <tr>
      <th>2</th>
      <td>PG-13</td>
    </tr>
    <tr>
      <th>3</th>
      <td>PG</td>
    </tr>
    <tr>
      <th>4</th>
      <td>G</td>
    </tr>
  </tbody>
</table>

> `Hints`:
- Use the film table
- Use SELECT * FROM film; to see what columns are available.
- Or use drop down table menu in pgadmin.

> `Solution`:

- View all the distinct rating from the `film` table

```sql
SELECT DISTINCT rating FROM film;
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NC-17</td>
    </tr>
    <tr>
      <th>1</th>
      <td>R</td>
    </tr>
    <tr>
      <th>2</th>
      <td>PG-13</td>
    </tr>
    <tr>
      <th>3</th>
      <td>PG</td>
    </tr>
    <tr>
      <th>4</th>
      <td>G</td>
    </tr>
  </tbody>
</table>

---

### 3. SELECT & WHERE

> [!NOTE]
> We now know enough to answer more relaistic business questions and tasks instead of directly asking for sepecific SQL tasks. Therefore, from now on we will be focusing more on directly asking the business related questions, to more realistically model a typical task.

<img src="../../images/challenge-shift.png"
    alt="Image Caption"
    style="border:1px solid white; padding:1px; background:#fff; width: 3000px;" />

> [!IMPORTANT]
> It is important to keep in mind that sooner or later, you are going to relaize that there are usually many different ways to arrive at the same solution. So it is also important to verify your own work against the expected result instead of the SQL solution provided by the course/lecturer.

*Now that we are on the same page, lets continue with the challenge*

---

> `Challenge 1`: 

- A customer forgot their wallet at our store! we need to track down their email to inform them.
- What is the email for the customer with the name 'Nancy Thomas'

> `Expected Answer`: 
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>nancy.thomas@sakilacustomer.org</td>
    </tr>
  </tbody>
</table>

> `Hints`:

- Use the customer table
- Make sure the capitalization and spelling of the names is correct
- use AND to combine conditions
- Use single quotes around the 'string'

> `Solution`:

```sql
SELECT email FROM customer
WHERE first_name = 'Nancy' AND last_name = 'Thomas';
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>nancy.thomas@sakilacustomer.org</td>
    </tr>
  </tbody>
</table>

---

> `Challenge 2`: 

- A customer wants to know what the movie "Outlaw Hanky" is about.
- Could you give them the description for the movie "Outlaw Hanky" ?

> `Expected Answer`: 
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A Thoughtful Story of a Astronaut And a Compos...</td>
    </tr>
  </tbody>
</table>

> `Hints`:

- Use the film table
- Make sure the capitalization and spelling of the movie name is correct
- use AND to combine conditions
- Use single quotes around the 'string'

> `Solution`:

```sql
SELECT description FROM film
WHERE title = 'Outlaw Hanky';
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A Thoughtful Story of a Astronaut And a Compos...</td>
    </tr>
  </tbody>
</table>

---

> `Challenge 3`: 

- A customer is late on their movie return, we've mailed them a letter to their address at '259 Ipoh Drive'. We should also called them on the phone to let them know.

- Can you get the phone number for the drive customer who lives at '259 Ipoh Drive'?

> `Expected Answer`: 

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>phone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>419009857119</td>
    </tr>
  </tbody>
</table>

> `Hints`:

- Use the address table
- Make sure the capitalization and spelling of the address is correct
- Use single quotes around the 'string'

> `Solution`:

```sql
SELECT phone FROM address 
WHERE address = '259 Ipoh Drive';
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>phone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>419009857119</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> A table can share the name with its own column. Example, in the above address table there is also a coumn named address.

---

### 4. ORDER BY