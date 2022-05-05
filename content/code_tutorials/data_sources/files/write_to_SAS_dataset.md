---
title: "Write to a SAS Dataset"
author: "Greg Barbieri"
date: 2022-04-23
description: "Write data as a SAS dataset."
type: "code_tutorials"
--- 

Write Pandas Data Frame to SAS dataset. Requires a SAS installation. [SASPy documentation](https://sassoftware.github.io/saspy/)

### Imports


```python
import os
import saspy
import pandas as pd
```

### Set PATH Environment Variable

Add the location of the sspiauth.dll file to the PATH environment variables. For those who are unable to edit environmental variables without administrative permissions, execute the following code at run time with the correct file location.


```python
os.environ["PATH"] += os.environ["PATH"][:-1] + 'C:\\SASHome\\SASFoundation\\9.4\\core\\sasext;'
```

### Create Pandas Data Frame


```python
df = pd.DataFrame(data=[['apple', 'iris', 'oak'],
                        ['grape', 'juniper', 'ash'],
                        ['strawberry', 'chamomile ', 'pine']],
                  columns=['fruit','flower','tree'])
```

### Start SAS Session

To start a SAS session, you may need to create and point to a personalized SAS configuration file. Instructions are [here](https://sassoftware.github.io/saspy/install.html#configuration). Most of the options in the template configuration file do not need to be edited. Just point to the correct SAS installation and use the correct configuration name.


```python
sas = saspy.SASsession(cfgfile='sascfg_personal.py')
```

    Using SAS Config named: winlocal
    SAS Connection established. Subprocess id is 18352
    


### Create Library Reference

SAS library reference uses the root directory by default. For Windows, that's likely the "C:\\" drive. Update path to your desired location.


```python
sas.saslib('libout', path="\\")
```

    
    19                                                         The SAS System                            09:39 Wednesday, March 23, 2022
    
    113        
    114        libname libout    '\'  ;
    NOTE: Libref LIBOUT was successfully assigned as follows: 
          Engine:        V9 
          Physical Name: C:\
    115        
    116        
    117        
    
    20                                                         The SAS System                            09:39 Wednesday, March 23, 2022
    
    118        


### Write to SAS Dataset

`df` is the Pandas Data Frame. `table` is the name of the output SAS dataset. `libref` is the output library reference. Equivalent to:

```sas
data libout.output_dataset;
    set work.df;
run;
```


```python
sas.dataframe2sasdata(df=df, table="output_dataset", libref='libout')
```




    Libref  = libout
    Table   = output_dataset
    Dsopts  = {}
    Results = Pandas



### End SAS Session


```python
sas.endsas()
```

    SAS Connection terminated. Subprocess id was 18352

