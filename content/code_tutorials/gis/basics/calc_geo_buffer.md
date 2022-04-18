---
title: "Calculate a Geographic Buffer"
author: "Greg Barbieri"
date: 2022-04-18
description: "Calculate a buffer around a geographic Area."
type: "code_tutorials"
--- 

Calculate a buffer around a geographic area.

### Imports


```python
import geopandas as gpd
import matplotlib.pyplot as plt
```

### Load State Shape File


```python
gdf_st = gpd.read_file(substate, geometry='geometry')
```

### Subset to Washington, DC

Convert to the CRS [EPSG 6933](https://epsg.io/6933). The main benefit: units are in meters.


```python
gdf_dc = gdf_st.loc[gdf_st['STUSPS'] == 'DC'].to_crs(epsg=6933)
```

### Find Buffer Around Polygon

Use `buffer` method to calculate the buffer around the polygon. Pass `1609` to `distance` to create a 1 mile buffer around the DC polygon.


```python
gdf_dc_buff = gdf_dc['geometry'].buffer(distance=(1609))
```

Plot DC polygon with and without the buffer. Both are using the same CRS, so the coordinates line up on the plot as expected.


```python
fig, ax = plt.subplots()

gdf_dc.plot(ax=ax)
gdf_dc_buff.plot(alpha=0.50, ax=ax)

plt.show()
```



![png](/images/calc_geo_buffer.png)
    

