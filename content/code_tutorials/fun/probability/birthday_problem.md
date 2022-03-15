---
title: "Birthday Problem"
author: "Greg Barbieri"
date: 2021-01-03
description: "Probability of two people having the same birthday."
type: "code_tutorials"
---

If there are n people in the room, the probability that all n birthdays are distinct equals (none are equal):

$\displaystyle\prod_{k=1}^{n}{\frac{365-(k-1)}{365}}$

Therefore, the probability is 1 minus the results of the product.

## Imports

```python
import numpy as np
import matplotlib.pyplot as plt
```

## Calculate Probability

```python
indiv_prob_list = []

for num in range(1,101):
    indiv_prob = (365-(num-1))/365
    
    indiv_prob_list.append(indiv_prob)
```

## Plot Probability

```python
plt.plot(np.linspace(1,100,100), 1-np.cumprod(indiv_prob_list))
```



![png](/images/birthday_problem.png)
    

