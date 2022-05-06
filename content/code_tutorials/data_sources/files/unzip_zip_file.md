---
title: "Unzip a ZIP File."
author: "Greg Barbieri"
date: 2022-04-22
description: "Extract files from a ZIP file."
type: "code_tutorials"
---

### Imports

```python
import zipfile
```
### Extract Zip File

```python
with zipfile.ZipFile("input_file.zip", "r") as f:
    f.extractall()
```
