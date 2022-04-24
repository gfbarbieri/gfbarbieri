---
title: "Linear Optimization with Scipy"
author: "Greg Barbieri"
date: 2022-04-23
description: "Linear optimization with Scpipy."
type: "code_tutorials"
---

Simple Linear Optimization

### Imports


```python
from scipy.optimize import linprog
```

### Define the Problem

Maximize the utility function $U(x) = 2 x_1 + 2 x_2$ subject to the budget constraint $4 x_1+ 4 x_2 = 40$.

### Build the Coefficient Matrix

Create a list where each element is the coefficient for each variable. This is the coefficient matrix.

**Note:** The `linprog` function *minimizes* the objective, but we want to *maximize* the objective. In order to do that, we want the negative of the objective function, that is $-1*U(x)$


```python
obj_coef = [-2, -2]
```

### Define the Constraints

Create two matrices. The first is the coefficient matrix of the variables and the second is a constant vector.


```python
con_coef = [[4, 4]]
con_b = [40]
```

### Maximize the Objective

The arguments `A_eq` and `b_eq` represent the coefficient matrix and constant matrix for the constraint function, respectively. If the constraint is an inequality, then use arguments `A_ub` and `b_ub` instead.


```python
res = linprog(obj_coef, A_eq=con_coef, b_eq=con_b)
```

In this situation, the price of $x_1$ equals the prices of $x_2$, so the optimal quantities are equal to 5 (perfect substitutes with equal price), shown in the array for key `x`. Utility, `fun`, is negative because of our transformation of the objective function.


```python
res
```




         con: array([9.24359156e-07])
         fun: -19.999999537820422
     message: 'Optimization terminated successfully.'
         nit: 3
       slack: array([], dtype=float64)
      status: 0
     success: True
           x: array([4.99999988, 4.99999988])


