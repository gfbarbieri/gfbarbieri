---
title: "Print Names of Geographic Layers"
author: "Greg Barbieri"
date: 2022-04-18
description: "Print the geography layers avaialble in a geo-database file."
type: "code_tutorials"
--- 

Print the name of the layers available a geo-database table.

### Imports


```python
import fiona
import os
```

### Determine Available Layers

For each file listed in the geo-database with the file extension .gdbtable, print the name of the layers available.


```python
for f in os.listdir(gdb_dir):
    f_name, f_ext = os.path.splitext(f)

    if f_ext == '.gdbtable':
        layers = fiona.listlayers(os.path.join(gdb_dir, f))
        print(f"{f_name} : {layers}")
```

    a00000001 : ['GDB_SystemCatalog']
    a00000002 : ['GDB_DBTune']
    a00000003 : ['GDB_SpatialRefs']
    a00000004 : ['GDB_Items']
    a00000005 : ['GDB_ItemTypes']
    a00000006 : ['GDB_ItemRelationships']
    a00000007 : ['GDB_ItemRelationshipTypes']
    a00000009 : ['Block_Group']
    a0000000a : ['State']
    a0000000b : ['County_Subdivision']
    a0000000c : ['Consolidated_City']
    a0000000d : ['Census_Tract']
    a0000000e : ['Census_Designated_Place']
    a0000000f : ['County']
    a00000010 : ['Incorporated_Place']

