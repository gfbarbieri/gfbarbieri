---
title: "Read Data from Text Files"
author: "Greg Barbieri"
date: 2022-04-22
description: "Read data from text files."
type: "code_tutorials"
---

### Imports

```python
import io
import pandas as pd
import requests
```

### Download Text File

Download [historical price data](http://download.bls.gov/pub/time.series/cu) as text files.


```python
response = requests.get("http://download.bls.gov/pub/time.series/cu/cu.data.1.AllItems")
```

### Create Pandas Data Frame

Use `io.StrongIO(response.text)` to access data stored in memory. Otherwise, pass the file path directly to Pandas. Use `read_csv` to create a Pandas Data Frame. This file is separated by tab characters ('\t').


```python
df = pd.read_csv(filepath_or_buffer=io.StringIO(response.text), sep='\t')
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
      <th>series_id</th>
      <th>year</th>
      <th>period</th>
      <th>value</th>
      <th>footnote_codes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CUSR0000SA0</td>
      <td>1947</td>
      <td>M01</td>
      <td>21.48</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CUSR0000SA0</td>
      <td>1947</td>
      <td>M02</td>
      <td>21.62</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CUSR0000SA0</td>
      <td>1947</td>
      <td>M03</td>
      <td>22.00</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CUSR0000SA0</td>
      <td>1947</td>
      <td>M04</td>
      <td>22.00</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CUSR0000SA0</td>
      <td>1947</td>
      <td>M05</td>
      <td>21.95</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>


