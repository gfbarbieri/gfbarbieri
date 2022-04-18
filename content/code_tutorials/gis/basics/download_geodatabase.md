---
title: "Download Geographic Databases"
author: "Greg Barbieri"
date: 2022-04-18
description: "Download geographic databases with documentation from the Census Bureau."
type: "code_tutorials"
--- 

Download Census Geo-database and the database documentation.

[TIGER Geodatabases](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-geodatabase-file.html) are spatial extracts from the Census Bureau MAF/TIGER database, designed for use with Esri’s ArcGIS. These files do not include demographic data, but they contain geographic entity codes that can be linked to Census Bureau demographic data, available on American FactFinder.

### Imports


```python
import requests
```

### Download Census Geodatabase


```python
response = requests.get('https://www2.census.gov/geo/tiger/TGRGDB18/tlgdb_2018_a_us_substategeo.gdb.zip')
```


```python
with open('census_gdb.zip', 'wb') as zf:
    zf.write(response.content)
```

### Download Census Geodatabase Documentation

Iterate over content with `iter_content` if the file is very large, otherwise `content` suffices without the for-loop.


```python
response = requests.get('https://www2.census.gov/geo/pdfs/maps-data/data/tiger/tgrshp2018/2018_TIGER_GDB_Record_Layouts.pdf')
```


```python
with open("Census_Geodatabase_Documentation.pdf", "wb") as pdf:
    for chunk in response.iter_content():
        pdf.write(chunk)
```
