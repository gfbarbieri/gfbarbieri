---
title: "Solve System of Linear Equations"
author: "Greg Barbieri"
date: 2022-04-23
description: "Solve a system of linear equations with Sympy."
type: "code_tutorials"
---

Solve basic systems of linear equations: [SymPy Documentation](https://docs.sympy.org/latest/modules/solvers/solveset.html#sympy.solvers.solveset.linsolve)

### Imports


```python
import sympy as sp
```

$$ 5x - y + 3z = 12 \\
3x + y + z = 2 \\
x + 2y + z = 0 $$

### Define System of Equations

Create system in $\textbf{A}\textbf{x}=\textbf{b}$ form.


```python
X = [5, -1, 3]
Y = [3, 1, 1]
Z = [1, 2, 1]
B = [12, 2, 0]

A = sp.Matrix([X, Y, Z])
b = sp.Matrix(B)

print(A,b)
```

    Matrix([[5, -1, 3], [3, 1, 1], [1, 2, 1]]) Matrix([[12], [2], [0]])


### Solve Linear System

Define variables.

```python
x, y, z = sp.symbols('x, y, z')
```

Solve using `linsolve`.


```python
sol = sp.linsolve((A,b), (x, y, z))

sol
```




$\displaystyle \left\{\left( \frac{1}{6}, \  - \frac{5}{3}, \  \frac{19}{6}\right)\right\}$


