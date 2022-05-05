---
title: "Extract Data from Word Documents."
author: "Greg Barbieri"
date: 2022-04-23
description: "Extract data from tables in a Word document."
type: "code_tutorials"
--- 

Extract data from a Microsoft Word document. Word documents are essentially XML files. Each Word document may present new wrangling challenges.

### Imports


```python
from docx import Document
import pandas as pd
```

### Find Tables in Word Document

Open a word file.


```python
doc = Document('file.docx')
```

Find the tables in the Word document.


```python
tables = doc.tables

print(f"There are {len(tables)} tables in this Word document.")
```

    There are 2 tables in this Word document.


### Extract Data

Extract data from each of the tables.


```python
data = []

for table in tables:
    table_data = []

    for row in table.rows:
        row_data = []

        for cell in row.cells:
            row_data.append(cell.text)

        table_data.append(row_data)
    
    data.append(table_data)
```

### Create Data Frame

Create a data frame from only the first table in the Word document.


```python
df = pd.DataFrame(data=data[0][1:], columns=data[0][0])
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Dates</th>
      <th>Employment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1/1/2000</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>


