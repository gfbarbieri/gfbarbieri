---
title: "Non-Linear Optimization with Scipy"
author: "Greg Barbieri"
date: 2022-04-23
description: "Non-linear optimization with Scipy."
type: "code_tutorials"
---

Optimize a Non-linear Function

### Imports


```python
from scipy.optimize import minimize
```

### Define the Problem

Maximize the utility function $U(x) = 2 x_1 x_2$ subject to the budget constraint $8 x_1+ 4 x_2 = 40$.

### Define the Objective Function

Create a Python function called `f` that takes in a vector called `x`, so `f(x)`. The vector `x` can be expected to have two elements, one for each subscript in the objective function. The Python function `f(x)` should return a value equal to the objective function.

**Note:** The `minimize` function *minimizes* the objective, but we want to *maximize* the objective. In order to maximize, multiply the objective function by -1.


```python
def f(x):
    return -1 * (2 * x[0] * x[1])
```

### Define the Constraint

Create a Python function called `constraints` that takes `x` as an argument and returns a value equal to the constraint function. If you have multiple constraints, you may be able to return the results of multiple functions without affecting the results. However, I recommend creating another constraint function.


```python
def constraint(x):
    return x[0]*8 + x[1]*4 - 40
```

### Maximize the Objective Function

Create the constraint dictionary `con` that contains details about each constraint function. The constraints here are equalities, so `type` is `eq`. The `fun` is short for "functions" and we set it equal to our constraint function. If you have multiple constraints, then create a list called `con` where each element is the constraint dictionary for each constraint function.


```python
con = {'type': 'eq', 'fun': constraint}
```

Define the starting point or initial guess to begin numerical algorithm. Length must be equal to the number of independent variables, in this case two. Use either all zero's or all one's, but there exists a literature on pre-searching techniques.


```python
x0 = [1, 1]
```

Optimize the objective function given constraints.


```python
res = minimize(f, x0=x0, constraints=con)
```

Optimal values of $x_1$ and $x_2$ are stored as an array in the key `x`. They should equal $x_1 = 2.5$, $x_2 = 5$. The utility of $U(2.5, 5) = 25$, stored in the key `fun` as a negative number because of our transformation to a maximization problem.


```python
res
```




         fun: -25.000000000000004
         jac: array([-10.,  -5.])
     message: 'Optimization terminated successfully'
        nfev: 12
         nit: 4
        njev: 4
      status: 0
     success: True
           x: array([2.49999999, 5.00000001])


