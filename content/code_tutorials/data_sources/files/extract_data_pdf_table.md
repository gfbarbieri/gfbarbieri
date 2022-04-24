---
title: "Extract Data from PDF Table."
author: "Greg Barbieri"
date: 2022-04-22
description: "Extract data from PDF table."
type: "code_tutorials"
--- 

Extract state-level [telephone usage estimates](https://www.cdc.gov/nchs/nhis/releases.htm#wireless) from a table in a PDF.

### Imports

```python
from bs4 import BeautifulSoup
import pandas as pd
from PyPDF2 import PdfFileReader
```

### Wrangling PDF Table

1. With `PdffileReader`, extract text from the first page of the PDF.
4. Find the tabular data. The line breaks are not in ideal places. This part will always require lots of trial and error.


```python
rows = []

with open("state-level-nhis-estimates.pdf", 'rb') as f:
    lines = PdfFileReader(f).getPage(0).extractText().splitlines()
    line_ranges = list(range(59,len(lines),16))
    
    for line in range(len(line_ranges)):
        if line == len(line_ranges) - 1:
            row = lines[line_ranges[line]:]
        else:
            row = lines[line_ranges[line]:line_ranges[line + 1]]
            
        for col in row:
            if col == ' ':
                row.remove(col)

        rows.append(row)
```

### Create Pandas Data Frame


```python
columns = ['Geographic Area','Wireless-only','Wireless-mostly',
           'Dual-use','Landline-mostly','Landline-only',
           'No Service','Total']

df = pd.DataFrame(data=rows, columns=columns)
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
      <th>Geographic Area</th>
      <th>Wireless-only</th>
      <th>Wireless-mostly</th>
      <th>Dual-use</th>
      <th>Landline-mostly</th>
      <th>Landline-only</th>
      <th>No Service</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A l aba m a</td>
      <td>52. 4 ( 2. 1)</td>
      <td>15. 1 ( 1. 5)</td>
      <td>13. 8 ( 1. 4)</td>
      <td>8. 8  ( 0. 8)</td>
      <td>6. 5  ( 0. 7)</td>
      <td>3. 3</td>
      <td>100. 0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A l a s k a</td>
      <td>51. 7 ( 2. 4)</td>
      <td>22. 0 ( 2. 0)</td>
      <td>15. 9 ( 1. 6)</td>
      <td>4. 9  ( 0. 7)</td>
      <td>3. 2  ( 0. 5)</td>
      <td>2. 3</td>
      <td>100. 0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A r i z ona</td>
      <td>63. 2  ( 1. 8)</td>
      <td>11. 5 ( 1. 2)</td>
      <td>11. 2 ( 1. 1)</td>
      <td>5. 2  ( 0. 6)</td>
      <td>4. 8  ( 0. 5)</td>
      <td>4. 1</td>
      <td>100. 0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A r k ans a s</td>
      <td>62. 8 ( 2. 2)</td>
      <td>12. 3 ( 1. 5)</td>
      <td>10. 0 ( 1. 3)</td>
      <td>6. 4  ( 0. 7)</td>
      <td>4. 2  ( 0. 6)</td>
      <td>4. 2</td>
      <td>100. 0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C al i f or ni a</td>
      <td>53. 0 ( 1. 1)</td>
      <td>18. 6 ( 0. 8)</td>
      <td>15. 1 ( 0. 7)</td>
      <td>6. 2  ( 0. 4)</td>
      <td>4. 3  ( 0. 2)</td>
      <td>2. 9</td>
      <td>100. 0</td>
    </tr>
  </tbody>
</table>
</div>


