---
title: "Query Oracle using Bind Variables"
author: "Greg Barbieri"
date: 2022-04-22
description: "Query an Oracle database using bind variables."
type: "code_tutorials"
--- 

Query Oracle Database with [Bind Variables](https://cx-oracle.readthedocs.io/en/latest/user_guide/bind.html)

### Imports


```python
import getpass
import cx_Oracle
```

### Establish Connection


```python
user_id = input('User ID: ')
password = getpass.getpass()

ora_conn = cx_Oracle.connect(user=user_id,
                             password=password,
                             dsn='<SERVICE NAME OR HOST/SERVICE>')

ora_conn.current_schema = '<SCHEMA>'
```

### Execute Query

Identify bind variables in query using `:<BIND VARIABLE>`. Pass value to the bind variable when executing the SQL.

**Bind Variable by Position**


```python
sql = """
SELECT c.*
  FROM <TABLE> c
 WHERE c.<COLUMN> IN (:<BIND VARIABLE 1>, :<BIND VARIABLE 2>)
"""

ora_cur = ora_conn.cursor()
ora_cur.execute(sql, ('<BV1 VALUE>','<BV2 VALUE>'))
```

**Bind Variable by Name**


```python
sql = """
SELECT c.*
  FROM <TABLE> c
 WHERE c.<COLUMN> IN (:KEY1, :KEY2)
"""

ora_cur = ora_conn.cursor()
ora_cur.execute(sql, {'KEY1':'VALUE1', 'KEY2':'VALUE2'})
```
