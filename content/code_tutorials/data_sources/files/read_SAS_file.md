---
title: "Read SAS Datasets"
author: "Greg Barbieri"
date: 2022-04-22
description: "Read SAS datasets."
type: "code_tutorials"
--- 

### Imports

```python
import pandas as pd
```

### Read SAS Dataset

Passing `encoding='latin-1'` has proved helpful in avoiding errors in string formats.


```python
df = pd.read_sas("input_dataset.sas7bdat", encoding='latin-1')
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
      <th>fruit</th>
      <th>flower</th>
      <th>tree</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>apple</td>
      <td>iris</td>
      <td>oak</td>
    </tr>
    <tr>
      <th>1</th>
      <td>grape</td>
      <td>juniper</td>
      <td>ash</td>
    </tr>
    <tr>
      <th>2</th>
      <td>strawberry</td>
      <td>chamomile</td>
      <td>pine</td>
    </tr>
  </tbody>
</table>
</div>


