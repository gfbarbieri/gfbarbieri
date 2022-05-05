---
title: "Unzip a Zip File."
author: "Greg Barbieri"
date: 2022-04-22
description: "Extract Zip files."
type: "code_tutorials"
--- 

### Imports

```python
import zipfile
```
### Extract Zip File

```python
with zipfile.ZipFile("AirQualityUCI.zip", "r") as f:
    f.extractall()
```
