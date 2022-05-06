---
title: "Download Text Files"
author: "Greg Barbieri"
date: 2022-04-22
description: "Download text files from the web."
type: "code_tutorials"
--- 

Download a [historical price data](http://download.bls.gov/pub/time.series/cu) published by the Bureau of Labor Statistics.

### Imports


```python
import requests
```

### Download Text File

Download data from `/cu.data.1.AllItems` as a text file.


```python
response = requests.get("http://download.bls.gov/pub/time.series/cu/cu.data.1.AllItems")
```


### Save as Text File


```python
with open('data.txt', 'w', newline='') as f:
    f.write(response.text)
```
