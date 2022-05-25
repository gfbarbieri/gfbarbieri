---
title: "Find Prices for Olive Oil Soap on Amazon"
author: "Greg Barbieri"
date: 2022-05-24
description: "Use Costco's warehouse locator to scrape warehouse information."
type: "code_tutorials"
---

Web scrape product prices from Amazon. In this example, I want to find the cheapest olive oil soap by price and by unit price. This example is involved and each wrangling step is not explained in detail.

### Imports


```python
import pandas as pd
import requests
from selenium import webdriver
```

### Amazon Text Search

Find the base URL of Amazon's text search by searching for someone on the Amazon website.


```python
base_url = 'https://www.amazon.com/s'
```

Infer from the results that `k` is the parameter that the text search is passed to, which I pass a parameter to the request.


```python
params = {'k':'olive oil soap'}
```

Create URL


```python
url = requests.Request('GET', base_url, params=params).prepare().url
```

Use Selenium WebDriver to create HTML.


```python
driver = webdriver.Chrome()
driver.get(url)
```

Part the HTML using Selenium. Each item for sale is stored in a container called `s-card-container`. I will perform some edits before creating the Pandas Data Frame.


```python
item = []

for wh in driver.find_elements_by_class_name('s-card-container'):
    # Pull the text data from the tags in the HTML class.
    container = wh.text.splitlines()

    # Those tags without text can be ignored.
    if not container:
        continue
    
    # If the first text is not a product name, then remove
    # the element from the list of text.
    if 'Sponsored' in container:
        container.remove('Sponsored')
    elif "Amazon's Choice" in container:
        container.remove("Amazon's Choice")

    # If the third item in the list isn't the price, then remove
    # the element from the list.
    if '$' not in container[2]:
        container.pop(2)
    
    # Finally, keep only the first 4 text fields.
    item.append(container[:4])
```

### Create Pandas Data Frame


```python
df = pd.DataFrame(data=item, columns=['product', 'size', 'price_whole', 'price_portion'])

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
      <th>product</th>
      <th>size</th>
      <th>price_whole</th>
      <th>price_portion</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Olive Oil Soap Bar - Handmade 100% Pure Natura...</td>
      <td>5.7 Ounce (Pack of 5)</td>
      <td>$14</td>
      <td>99 ($0.53/Ounce)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Kiss My Face Antibacterial Olive Oil Bar Soap,...</td>
      <td>8 Ounce (Pack of 1)</td>
      <td>$4</td>
      <td>29 ($0.54/Ounce)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Peet Bros | Olive Oil Moisturizing Bath Soap B...</td>
      <td>23</td>
      <td>$6</td>
      <td>99 ($1.40/Ounce)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Castile Soap Beauty Soap With Olive Oil, 3.9 O...</td>
      <td>3.9 Ounce (Pack of 6)</td>
      <td>$14</td>
      <td>07 ($0.60/Ounce)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kiss My Face 3 Pack Pure Olive Oil Vegan Bar S...</td>
      <td>3 Count (Pack of 1)</td>
      <td>$5</td>
      <td>99 ($0.50/Ounce)</td>
    </tr>
  </tbody>
</table>
</div>



### Edit Price and Unit Data

Standardize the price and unit data as best as possible and drop duplicates.


```python
df['price'] = df['price_whole'].str.split('$').str[1] + '.' + df['price_portion'].str[:2]
df['price_per_unit'] = df['price_portion'].str.split('$').str[1].str.split('/').str[0]
df['unit'] = df['price_portion'].str.split('/').str[1].str.split(')').str[0]

df.drop(columns=['size','price_whole','price_portion'], inplace=True)
df.drop_duplicates(inplace=True)
```

### Find Cheapest Product

Cheapest item by price.


```python
df.loc[df['price'].astype('float') == df['price'].astype('float').min()]
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
      <th>product</th>
      <th>price</th>
      <th>price_per_unit</th>
      <th>unit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Kiss My Face Antibacterial Olive Oil Bar Soap,...</td>
      <td>4.29</td>
      <td>0.54</td>
      <td>Ounce</td>
    </tr>
  </tbody>
</table>
</div>



Cheapest item by unit price.


```python
df.loc[df['price_per_unit'].astype('float') == df['price_per_unit'].astype('float').min()]
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
      <th>product</th>
      <th>price</th>
      <th>price_per_unit</th>
      <th>unit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>57</th>
      <td>Organic Olive Oil Hand Soap - Made with Natura...</td>
      <td>38.99</td>
      <td>0.30</td>
      <td>Fl Oz</td>
    </tr>
  </tbody>
</table>
</div>



### Close Browser, End Session


```python
driver.close()
driver.quit()
```
