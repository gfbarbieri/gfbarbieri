---
title: "Download Zip Files"
author: "Greg Barbieri"
date: 2022-04-22
description: "Download Zip files from the web."
type: "code_tutorials"
--- 

### Imports

```python
import requests
```

### Download ZIP file

Download the ZIP file using the `requests` library.


```python
url = "https://archive.ics.uci.edu/ml/machine-learning-databases/00360/AirQualityUCI.zip"

response = requests.get(url)
```

Write data to disk.


```python
with open("AirQualityUCI.zip", "wb") as f:
    f.write(response.content)
```
