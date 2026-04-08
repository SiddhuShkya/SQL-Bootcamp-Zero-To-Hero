## Extra: PostgreSQL With Python

In this section of the course, we'll have a quick overview of how to use the psycopg2 library with Python to interact with a database in PostgreSQl with Python. Please note: this section assumes that we already know Python and are able to download libraries using Python.

To get started go ahead and download the pyscopg2 library. You can follow the instructions for downloading it here:

> Download Instructions Here: [Installation - psycopg 3.3.4.dev1 documentation](https://www.psycopg.org/psycopg3/docs/basic/install.html)

> Pscyopg2 Tutorial Here: [Psycopg2 Tutorial - PostgreSQL wiki](https://wiki.postgresql.org/wiki/Psycopg2_Tutorial)

Or, you can simply run the below command using your terminal.

```text
pip install psycopg2-binary
```

> [!NOTE]
> We'll be using the Jupyter Notebook system to show the Python code used here, but you can follow along using any editor you prefer.

*A .py file and a .ipynb file are attached to this lecture as a reference for you!*

Let's get started!

> Import the necessary dependencies.

```python
## Cell 1

import os
import psycopg2 as pg2
from dotenv import load_dotenv
```

> Load the secret postgres password needed to connect our postgresql server.

```python
## Cell 2

# Load environment variables from .env file
load_dotenv()
# Get the PostgreSQL password from environment variables
postgres_password = os.getenv("POSTGRES_PASSWORD")
```

> Connect to our local postgresql server using psycopg2.

```python
## Cell 3

conn = pg2.connect(
    host="localhost",
    database="dvdrental",
    user="postgres",
    password=postgres_password
)
```

> Create a connection object and store it in a variable named 'cursor'.

```python
## Cell 4

cursor = conn.cursor()
```

> Execute an SQL query using the cursor object adnd display the returned result.

- Fetch the first row of the `payment` table.

```python
## Cell 5

cursor.execute('SELECT * FROM payment')
result = cursor.fetchone() 
result
```
```text
(17503,
 341,
 2,
 1520,
 Decimal('7.99'),
 datetime.datetime(2007, 2, 15, 22, 25, 46, 996577))
```

- Fetch the first 5 rows of the `payment` table.

```python
## Cell 6

result = cursor.fetchmany(5)
result
```
```text
[(17504,
  341,
  1,
  1778,
  Decimal('1.99'),
  datetime.datetime(2007, 2, 16, 17, 23, 14, 996577)),
 (17505,
  341,
  1,
  1849,
  Decimal('7.99'),
  datetime.datetime(2007, 2, 16, 22, 41, 45, 996577)),
 (17506,
  341,
  2,
  2829,
  Decimal('2.99'),
  datetime.datetime(2007, 2, 19, 19, 39, 56, 996577)),
 (17507,
  341,
  2,
  3130,
  Decimal('7.99'),
  datetime.datetime(2007, 2, 20, 17, 31, 48, 996577)),
 (17508,
  341,
  1,
  3382,
  Decimal('5.99'),
  datetime.datetime(2007, 2, 21, 12, 33, 49, 996577))]
```

> Close the connection.

```python
## Cell 7

cursor.close()
```

---

# <div align="center">Thank You for Going Through This Guide! 🙏✨</div>