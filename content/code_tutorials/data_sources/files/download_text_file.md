---
title: "Download Text Files"
author: "Greg Barbieri"
date: 2022-04-22
description: "Download text files from the web."
type: "code_tutorials"
--- 

### Imports


```python
import requests
```

### Download Text File

The Bureau of Labor Statistics makes some [historical price data](http://download.bls.gov/pub/time.series/cu) available as text files. `/cu.data.1.AllItems` is a text file with historical price data.


```python
response = requests.get("http://download.bls.gov/pub/time.series/cu/cu.data.1.AllItems")
```

### Save as Text File

Convert response to text.


```python
cpi_text = response.text
```

Write to drive.


```python
with open('data.txt', 'w', newline='') as f:
    f.write(cpi_text)
```
