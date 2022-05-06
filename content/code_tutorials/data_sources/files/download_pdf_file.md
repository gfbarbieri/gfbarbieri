---
title: "Download PDF Files"
author: "Greg Barbieri"
date: 2022-04-22
description: "Download PDF files."
type: "code_tutorials"
---

Download a PDF file from the web.

### Imports

```python
from PyPDF2 import PdfFileReader
import requests
```

### Download PDF Content


```python
url = "http://sites.nationalacademies.org/cs/groups/dbassesite/documents/webpage/dbasse_194828.pdf"
```


```python
response = requests.get(url)
```

### Write PDF Content to File

Use `.iter_content()` for large files or streaming.


```python
with open("data_day.pdf", "wb") as pdf:
    pdf.write(response.content)
```
