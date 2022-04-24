---
title: "Write to SQLite3 Table"
author: "Greg Barbieri"
date: 2022-04-23
description: "Output data to a SQLite3 database table."
type: "code_tutorials"
--- 

[Write to table](https://www.sqlitetutorial.net/sqlite-python/insert/) in SQLite database.

### Imports


```python
import sqlite3
import pandas as pd
```

### Create Pandas Data Frame


```python
df = pd.DataFrame(data=[['apple','iris','oak']],
                  columns=['fruit','flower','tree'])
```

### Connect to SQLite database

If database file does not exist, it will be created.


```python
db = sqlite3.connect("sqlite.db")
```

### Insert Pandas DataFrame into Database

Insert into database.

`con` is the SQLite database connection. `name` is the name of the table in the SQLite database. `if_exists` determines how to handle inserting data conditional on the table existing or not.


```python
df.to_sql(con=db, name='species', if_exists='append')
```

### Insert Data as Tuple

Create cursor.


```python
cur = db.cursor()
```

Create table `species` if it does not exist.


```python
sql = """
CREATE TABLE IF NOT EXISTS species (fruit, flower, tree);
"""
```

Insert rows into the table `species`. `?` are place holders for row data, ordered by column left to right.


```python
sql = """
INSERT INTO species(fruit, flower, tree)
     VALUES (?,?,?)
"""
cur = conn.cursor()
cur.execute(sql, ('apple', 'iris', 'oak'))
```

Commit the changes to the database using the connection object, not the cursor object.


```python
db.commit()
```

Confirm that table exists by viewing all tables in the database.


```python
sql = """
SELECT name 
  FROM sqlite_master
 WHERE type = 'table'
"""

cur.execute(sql)
tables = cur.fetchall()
print(tables)
```

Close the connection.


```python
conn.close()
```
