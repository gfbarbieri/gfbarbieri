---
title: "Find Difference Between Geographies"
author: "Greg Barbieri"
date: 2022-04-18
description: "Use overlay to find overlapping geographies."
type: "code_tutorials"
--- 

GIS intersection using overlay.

### Imports


```python
import geopandas as gpd
```

### Import Shape Files

Import the U.S. State shape file and the U.S. Urban Area shape file.


```python
gdf_st = gpd.read_file(substate, geometry='geometry')
gdf_ua = gpd.read_file(national, geometry='geometry')
```

### Subset Shape Files

Subset to Virginia


```python
gdf_st_va = gdf_st.loc[gdf_st['STUSPS'] == 'VA'].reset_index(drop=True)
```

Subset to Washington, DC urban area.


```python
gdf_ua_wdc = gdf_ua.loc[gdf_ua['NAMELSAD'] == 'Washington, DC--VA--MD Urbanized Area'].reset_index(drop=True)
```

### Overlay

Create a new shape which is the Washington, DC Urban Area without Virginia by passing `difference`.


```python
gdf_ua_wo_va = gpd.overlay(gdf_ua_wdc, gdf_st_va, how='difference').reset_index(drop=True)
```

What proportion of the original urban area is remaining?

First, convert to the CRS [EPSG 6933](https://epsg.io/6933) so that your coordinate system has units in meters. Second, use `area` method to calculate the area in square meters.


```python
gdf_ua_wo_va.to_crs(epsg=6933).area[0] / gdf_ua_wdc.to_crs(epsg=6933).area[0]
```




    0.47590796724518697


