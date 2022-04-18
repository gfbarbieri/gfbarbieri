---
title: "Load a Geographic Layer"
author: "Greg Barbieri"
date: 2022-04-18
description: "Load geography layers from a geo-database or shape file."
type: "code_tutorials"
--- 

Load a layer from a geo-database table or shape file using GeoPandas.

### Imports


```python
import geopandas as gpd
```

### Load Shape File

Census shape files usually store long-lat coordinates in a column called 'geometry'. Pass `geometry` to `geometry` argument.

CRS stands for Coordinate Reference System. This tells GeoPandas how you coordinates relate to one another, which is important for visualizations and calculations. EPSG:4326 is for WGS84 Latitude/Longitude, a common projection. Pass `ESPG:4326` to `crs` argument.


```python
gdf = gpd.read_file(gdb_dir, geometry='geometry', crs='EPSG:4326')
```


```python
gdf.head()
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
      <th>COUNTYNS</th>
      <th>GEOID</th>
      <th>NAMELSAD</th>
      <th>CLASSFP</th>
      <th>FUNCSTAT</th>
      <th>ALAND</th>
      <th>AWATER</th>
      <th>INTPTLAT</th>
      <th>INTPTLON</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00161526</td>
      <td>01001</td>
      <td>Autauga County</td>
      <td>H1</td>
      <td>A</td>
      <td>1.539634e+09</td>
      <td>2.567481e+07</td>
      <td>+32.5322367</td>
      <td>-86.6464395</td>
      <td>MULTIPOLYGON (((-86.90310 32.54063, -86.90311 ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00161527</td>
      <td>01003</td>
      <td>Baldwin County</td>
      <td>H1</td>
      <td>A</td>
      <td>4.117656e+09</td>
      <td>1.132956e+09</td>
      <td>+30.6592183</td>
      <td>-87.7460666</td>
      <td>MULTIPOLYGON (((-87.99068 30.55549, -87.99051 ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00161528</td>
      <td>01005</td>
      <td>Barbour County</td>
      <td>H1</td>
      <td>A</td>
      <td>2.292160e+09</td>
      <td>5.052321e+07</td>
      <td>+31.8702531</td>
      <td>-85.4051035</td>
      <td>MULTIPOLYGON (((-85.42982 32.04598, -85.42985 ...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00161529</td>
      <td>01007</td>
      <td>Bibb County</td>
      <td>H1</td>
      <td>A</td>
      <td>1.612189e+09</td>
      <td>9.572303e+06</td>
      <td>+33.0158929</td>
      <td>-87.1271475</td>
      <td>MULTIPOLYGON (((-87.31226 33.08622, -87.31218 ...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00161530</td>
      <td>01009</td>
      <td>Blount County</td>
      <td>H1</td>
      <td>A</td>
      <td>1.670259e+09</td>
      <td>1.486028e+07</td>
      <td>+33.9773575</td>
      <td>-86.5664400</td>
      <td>MULTIPOLYGON (((-86.74919 33.99760, -86.74902 ...</td>
    </tr>
  </tbody>
</table>
</div>


