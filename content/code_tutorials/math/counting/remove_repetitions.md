---
title: "Remove Repetitions"
author: "Greg Barbieri"
date: 2017-08-26
description: "Removing repetitions, avoiding double counting."
type: "code_tutorials"
--- 

This question comes from Professor David Morin's book, <a href="http://www.people.fas.harvard.edu/~djmorin/book.html">Probability For the Enthusiastic Beginner</a>, Chapter 1, page 26.

1. We know that the number of ordered sets of three people chosen from five people is $5 \times 4 \times 3 = 60$. Reproduce this results by starting with the naive answer of $5^3 = 125$ ordered sets where repetitions are allowed, and then subtracting off the number of triplets that have repeated people.

### Imports

```python
import itertools
import pandas as pd
```

The naive answer comes from the formula $N^{k}$, where we want to select $k$ people from $N$ people, hence $5^3 = 125$. The answer without repetitions comes from the following formula: $$\frac{N!}{(N-k)!} = \frac{5!}{(5-3)!} = \frac{5!}{2!} = 5 \times 4 \times 3 = 60$$

```python
people = ['P1', 'P2', 'P3', 'P4', 'P5']

perm_w_rep = list(itertools.product(people, repeat=3))

len(perm_w_rep)
```




    125

### Remove Repetitions

Remove repetitions from all permutations from the list of tuples. Reverse the list if you are going to remove elements while iterating over the list.

```python
for order in reversed(perm_w_rep):
    if (order[0] == order[1]) or (order[0] == order[2]) or (order[1] == order[2]):
        perm_w_rep.remove(order)

len(perm_w_rep)
```

    60

Instead, search a Data Frame for repetitions.

```python
df = pd.DataFrame(perm_w_rep, columns = ['First', 'Second', 'Third'])

df = df[((df_perm_w_rep['First'] != df_perm_w_rep['Second']) & 
         (df_perm_w_rep['First'] != df_perm_w_rep['Third']) & 
         (df_perm_w_rep['Second'] != df_perm_w_rep['Third']))]

len(df)
```

    60