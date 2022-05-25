---
title: "Locate Costco Warehouses"
author: "Greg Barbieri"
date: 2022-05-24
description: "Use Costco's warehouse locator to scrape warehouse information."
type: "code_tutorials"
---

Use Costco's store locator to find the location of stores programmatically. Web scraping involves many technical issues unique to each website. If the website changes slightly, the entire program could become worthless.

### Imports


```python
import requests
from selenium import webdriver
```

### Open Store Locator

Infer the structure of Costco's store locator URL by going to Costco's website and using the tool.


```python
base_url = 'https://www.costco.com/warehouse-locations'
```

Use Requests library to build the URL without requesting the HTML. The search parameter is called `1ocation`.


```python
params = {'location': 'WASHINGTON DC'}
url = requests.Request('GET', base_url, params=params).prepare().url
```

Use Selenium to open Google Chrome to Costco's store locator for Washington, DC. Must pass the path to ChromeDriver directly or set the location in your system path.


```python
driver = webdriver.Chrome()
driver.get(url)
```

### Get Warehouse Name and URL

Inspecting Costco's store locator, we can find the list of warehouses at the URL using the class tag `warehouse-name`.


```python
whlst = [(wh.text, wh.get_property('href')) for wh in driver.find_elements_by_class_name('warehouse-name')]
```


```python
whlst[0]
```




    ('Pentagon City',
     'https://www.costco.com/warehouse-locations/pentagon-city-arlington-va-233.html')



Print the first warehouse.


```python
print(whlst[0])
```

    ('Pentagon City', 'https://www.costco.com/warehouse-locations/pentagon-city-arlington-va-233.html')


### Get Warehouse Addresses

Using the id tag `warehouse-list` we can find the address information, as well as other ancillary information associated with the store location. I will leave further data wrangling up to the user.


```python
whloc = driver.find_element_by_id('warehouse-list').text.splitlines()
```


```python
whloc[:5]
```




    ['1',
     'Pentagon City (2.88 mi)',
     '1200 S FERN ST',
     'ARLINGTON, VA 22202-2862',
     '(703) 413-2324']



### Close Browser, End Session


```python
driver.close()
driver.quit()
```
