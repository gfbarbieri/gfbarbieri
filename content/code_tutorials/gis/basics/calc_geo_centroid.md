---
title: "Calculate a Geographic Centroid"
author: "Greg Barbieri"
date: 2022-04-18
description: "Calculate the centroid of a geographic area."
type: "code_tutorials"
--- 

Calculate centroid of a geographic area.

### Imports


```python
import geopandas as gpd
import matplotlib.pyplot as plt
```

### Load Shape File


```python
gdf_st = gpd.read_file(substate, geometry='geometry')
```

### Subset to Washington, DC


```python
gdf_dc = gdf_st.loc[gdf_st['STUSPS'] == 'DC']
```

### Calculate Centroid


```python
gdf_dc_ct = gdf_dc.centroid
```

### Plot


```python
fig, ax = plt.subplots()

gdf_dc.plot(ax=ax)
gdf_dc_ct.plot(ax=ax, color='yellow')
```




    <AxesSubplot:>




    
![png](calc_geo_centroid.png)
    

