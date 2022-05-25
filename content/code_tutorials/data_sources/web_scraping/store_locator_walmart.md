---
title: "Locate Walmart Stores"
author: "Greg Barbieri"
date: 2022-05-24
description: "Use Walmart's store locator to scrape warehouse information."
type: "code_tutorials"
---

Use Walmart's store locator to find the location of stores programmatically. Web scraping involves many technical issues unique to each website. If the website changes slightly, the entire program could become worthless.

### Imports


```python
from bs4 import BeautifulSoup
import json
import requests
```

### Walmart Store Locator

Find the base URL of Walmart's store locator.


```python
base = 'https://www.walmart.com/store/finder'
```

Since Walmart does not return Java that must be loaded by a browser, we can use Requests library to pull the HTML directly. Also, parameters are `location` and `distance`.


```python
headers = {'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/98.0.4758.102 Safari/537.36'}

params = {'location':'washington dc',
          'distance':'50'}
```

Use Requests library to retrieve HTML from the URL with the parameters Washington DC and 50 miles.


```python
response = requests.get(url=base,
                        params=params,
                        headers=headers)
```

### Parse the HTML

Use BeautifulSoup to parse the HTML.


```python
articles = BeautifulSoup(response.text)
```

The id tag `storeFinder`, return the list of stores.


```python
artcl_str = articles.find(id='storeFinder').string
```

The resulting list is formatted as JSON. Use JSON to parse the store list.


```python
artcl_json = json.loads(artcl_str)
```

### Parse the JSON

From here, parse the JSON as you would a Python dictionary.


```python
stores_dict = artcl_json['storeFinder']['storeFinderCarousel']['stores']
```

Print the address of the first store. I will leave further wrangling and storing of data to the user.


```python
stores_dict[0]['address']
```




    {'postalCode': '20001',
     'address': '99 H Street Nw',
     'city': 'Washington',
     'state': 'DC',
     'country': 'US'}


