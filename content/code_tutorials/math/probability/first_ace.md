---
title: "First Ace"
author: "Greg Barbieri"
date: 2022-04-18
description: "Probability nth card is the first ace dealt."
type: "code_tutorials"
---

You are dealt a 5 card hand with an ace. What is the probability that the first ace you are dealt is in the Nth card?

### Import


```python
import numpy as np
import matplotlib.pyplot as plt
import itertools
```

### Create Deck of Cards

We can ignore suits.


```python
cards = np.array(['2','3','4','5','6','7','8','9','T','J','Q','K','A'])

cards = np.repeat(cards, 4)
```

### Find Location of the First Ace Dealt

There are over 300 million permutations of 5-card hands. Don't create them all and check each hand. Instead, approximate the answer by checking the location of the first ace in 1,000,000 randomly generated 5-card hands.


```python
first_ace = []

for i in range(0,1000000):
    hand = np.random.choice(cards, 5)

    if np.any(np.isin(hand, 'A')):
        first_ace.append(np.min(np.where(np.isin(hand, 'A'))))
```

### Count Location of First Ace Dealt

Produce a count by location of the first ace dealt in the hand. Python indexes at 0, so the location of the ace is the index plus one.


```python
unique, counts = np.unique(first_ace, return_counts=True)
```

### Plot Probability

The probability decreases with each card dealt.


```python
plt.bar(unique + 1, counts/len(first_ace))

plt.title("Probability; Conditional on Dealing an Ace")
plt.xlabel("Nth Card Dealt an Ace")
plt.ylabel("Probability")

plt.show()
```


    
![png](output_10_0.png)
    

