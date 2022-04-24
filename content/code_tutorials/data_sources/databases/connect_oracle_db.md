---
title: "Connect to an Oracle Database"
author: "Greg Barbieri"
date: 2022-04-22
description: "Connect to an Oracle database."
type: "code_tutorials"
--- 


Connect to [Oracle database](https://cx-oracle.readthedocs.io/en/latest/user_guide/connection_handling.html).

If a service name is defined in the tsanames.ora configuration file (C:\\\<oracle roots>\network\admin), then pass the service name to `dsn`. Otherwise, create the full URL and pass it to `dsn`: 'host:port/service_name'. See [documentation](https://cx-oracle.readthedocs.io/en/latest/user_guide/connection_handling.html) for more details.

### Imports


```python
import cx_Oracle
import getpass
```

### Establish Connection

Retrieve username and password.


```python
user_id = input()
password = getpass.getpass()
```


```python
or_conn = cx_Oracle.connect(user=user_id,
                            password=password,
                            dsn='<SERVICE NAME or HOST:PORT/SERVICE_NAME>')

or_conn.current_schema = '<SCHEMA>'
```
