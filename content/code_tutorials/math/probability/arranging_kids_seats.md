---
title: "Arranging Kids in Seats"
author: "Greg Barbieri"
date: 2022-04-18
description: "Counting possible arrangements of people in seats."
type: "code_tutorials"
---

This introductory question comes directly from <a href="http://www.people.fas.harvard.edu/~djmorin/book.html">Probability For the Enthusiastic Beginner</a>, Chapter 1, page 26.

1. Six girls and four boys are to be assigned to ten seats in a row, with the stipulations that a girl sits in the third seat and a boy sits in the eighth seat. How many arrangements are possible?

## Imports


```python
import itertools
```

### Create All Possible Arrangements

The length of our list confirms the expected number of arrangements.

Ignoring the stipulations, assuming no replacement, and order matters, we epxect $3,628,800$ possible outcomes with those satisfying the stipulations being a subset.

$$\frac{N!}{(N-n)!} = \frac{10!}{(10-10)!} = 10! = 3,628,800$$


```python
lst = ['G', 'G', 'G', 'G', 'G', 'G', 'B', 'B', 'B', 'B']

all_arrangements = list(itertools.permutations(lst, 10))

len(all_arrangements)
```




    3628800



### Apply Stipulations

Count the number of arrangements where the 8th element of the arrangement is a “B” and the 3rd element of the arrangement is a “G” (elements in a Python list are indexed at 0).


```python
stipulations = 0

for arrangement in all_arrangements:
    if arrangement[7] == "B" and arrangement[2] == "G":
        stipulations += 1
        
stipulations
```




    967680


