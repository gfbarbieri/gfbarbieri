---
title: "Non-Linear Optimizaiton with Sympy"
author: "Greg Barbieri"
date: 2022-04-23
description: "Non-linear optimization with Sympy (Lagrangian)."
type: "code_tutorials"
---

Find optimal values of x and y using symbolic methods.

### Imports


```python
import sympy as sp
```

### Define Variables


```python
x, y, p_x, p_y, l = sp.symbols('x y p_x p_y lambda')
```

### Define Objective and Constraint Functions


```python
f = 2*x*y
```


```python
g = 40 - p_x*x - p_y*y
```

### Define Lagrangian


```python
L = f + l*g
```

### Find First Order Conditions


```python
L_x = sp.diff(L,x)
L_y = sp.diff(L,y)
L_l = sp.diff(L,l)
```

### Solve for Optimal Values


```python
solu = sp.solve([L_x, L_y, L_l], [x, y, l], dict=True)

solu
```




    [{x: 20/p_x, y: 20/p_y, lambda: 40/(p_x*p_y)}]



Solve for $p_x =4$ and $p_y = 8$.


```python
p_vr = {p_x:4, p_y:8}

print(solu[0][x].subs(p_vr), solu[0][y].subs(p_vr))
```

    5 5/2

