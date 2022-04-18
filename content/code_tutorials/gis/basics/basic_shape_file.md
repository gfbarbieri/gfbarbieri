---
title: "Manipulate Shape Files"
author: "Greg Barbieri"
date: 2022-04-18
description: "Basic shape file manipulations."
type: "code_tutorials"
--- 

Basic ESRI Shape File tasks using GeoPandas: import, edit, plot, export shape files.

### Imports


```python
import geopandas as gpd
```

### Import Shape File


```python
gdf = gpd.read_file("us_county.shp")
```

### Edit Shape File


```python
gdf = gdf.loc[gdf['STATEFP'] == '31']
```

### Plot Shape File


```python
gdf.plot()
```




    <AxesSubplot:>




    
![png](/images/basic_shape_file.png)
    


### Export Shape File

Export creates all 5 files: .cpg, .dbf, .prj, .shp, .shx.


```python
gdf.to_file('us_state_31.shp')
```
