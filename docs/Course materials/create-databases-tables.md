## Creating Databases & Tables

This guide covers a set of powerful SQL techniques that go beyond the basics, helping you write more expressive, efficient, and flexible queries. What's covered:

1. Data Types
2. Primary & Foreign Keys
3. Constraints
4. CREATE, INSERT, UPDATE
5. DELETE, ALTER & DROP

When creating a database and table, take your time to plan for long term storage. Remember you can always remove historical you've decided you aren't using, but you can't go back in time to add in information!

> [!NOTE]
> Always do a quick google search for best practices, and definitely refer the documentation to see your full range of options.

> Documentation here : [PostgreSQL Documentation: Data Types](https://www.postgresql.org/docs/current/datatype.html)

---

> View all from `payment` table.

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

- Primary Key : payment_id
- Foreign Keys : ??????

> Check if there are foreign keys in the `payment` table using the pgAdmin.

1. From the left side panel that shows the servers. Expand the tabs following the below pattern

```text
Servers → Local DB (Your Server Name) → databases → dvdrental → schemas → public → Tables → payment → Constraints
```

<img src="../../images/payment-constraints.png"
    alt="Image Caption"
    style="border:1px solid white; padding:1px; background:#fff; width: 3000px;" />

2. You will see the below list:

- payment_customer_id_fkey
- payment_pkey
- payment_rental_id_fkey
- payment_staff_id_fkey

*The **_pkey** represents the primary key for the payment table. Similarly the **_fkey** represents the foreign key for the payment table.*

3. Therefore for the `payment` table,

- Primary key : payment_id
- Foreign Keys : customer_id, staff_id, rental_id

4. Select one of the foreign key (I selected customer_id) and right click it. Then click on properties and then left click on columns tab.

<img src="../../images/payment-customer-id-key.png"
    alt="Image Caption"
    style="border:1px solid white; padding:1px; background:#fff; width: 3000px;" />

*You should see a table named columns with headings : Local, Referenced, Referenced Table*

> Refererence Table has the value **public.customer**, meaning that the foreign key customer_id of the `payment` table is referencing to the primary key of the `customer` table.