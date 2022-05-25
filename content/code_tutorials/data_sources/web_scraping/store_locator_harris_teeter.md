---
title: "Locate Harris Teeter Stores"
author: "Greg Barbieri"
date: 2022-05-24
description: "Use Harris Teeter's store location to scrape store information."
type: "code_tutorials"
---

Use Harris Teeter's store locator to find the location of stores programmatically. Web scraping involves many technical issues unique to each website. If the website changes slightly, the entire program could become worthless.

### Imports


```python
import requests
from selenium import webdriver
```

### Open Store Locator

Infer the structure of Harris Teeter's store locator URL by going to the website and using the tool.


```python
base_url = 'https://www.harristeeter.com/stores/search'
```

Use Requests library to build the URL without requesting the HTML. The location parameter is called `searchText`. To cycle through pages, use the parameter `selectedPages`. Again, this can all be discovered by using the tool.


```python
params = {'searchText': 'Washington DC'}
url = requests.Request('GET', base_url, params=params).prepare().url
```

Use Selenium to open Google Chrome to Costco's store locator for Washington, DC. Must have ChromeDriver available.


```python
driver = webdriver.Chrome()
driver.get(url)
```

### Find Store Locations

Using the class tag `StoreSearchResult-columnTwo`, compile each store name on the first page of the search results.


```python
stloc = [loc.text.splitlines() for loc in driver.find_elements_by_class_name('StoreSearchResult-columnTwo')]
```


```python
stloc[0]
```




    ['Constitution Square',
     '1.2 miles',
     '1201 First St NE Washington, DC 20002Get Directions',
     '(202) 589-0351',
     'OPEN UNTIL 10:00 PM',
     'Browse this store online',
     'View Store Details',
     'View Weekly Ad']



### Close Browser, End Session


```python
driver.close()
driver.quit()
```
