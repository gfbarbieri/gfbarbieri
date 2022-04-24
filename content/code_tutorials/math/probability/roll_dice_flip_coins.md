---
title: "Roll Dice, Flip Coins"
author: "Greg Barbieri"
date: 2022-04-18
description: "Counting possible outcomes of rolling dice and flipping coins."
type: "code_tutorials"
---

This question comes from Professor David Morin's book, <a href="http://www.people.fas.harvard.edu/~djmorin/book.html">Probability For the Enthusiastic Beginner</a>, Chapter 1, page 26.

1. One person rolls two six-sided dice, and another person flips six two-sided coins. Which setup has the larger number of possible outcomes, assuming that the order matters?

### Imports


```python
import itertools
```

### Roll Two Six-Sided Dice

Create a list representing a six-sided die.


```python
die = ['1','2','3','4','5','6']
```

If you prefer the statement “rolling two six-sided die once”, then create all possible outcomes of rolling two identical die, returning a Cartesian product of the list die and itself.


```python
dice_permutations = list(itertools.product(die, die))
```

If you prefer the statement "rolling one six-sided die twice", then create all possible outcomes using the repeat option.


```python
dice_permutations = list(itertools.product(die, repeat=2))
```

Both return the same outcome.


```python
list(itertools.product(die, die)) == list(itertools.product(die, repeat=2))
```




    True



### Flip Six Two-Sided Coins

Create a list representing the two outcomes of flipping a coin.


```python
coin = ['H','T']
```

If you prefer the concept of flipping six two-sided coins, then list all six coins.


```python
coin_permutations = list(itertools.product(coin, coin, coin, coin, coin, coin))
```

If you prefer of flipping one two-sided coin six times, then using the repeat option.


```python
coin_permutations = list(itertools.product(coin, repeat=6))
```

Again, they're identical.


```python
list(itertools.product(coin, coin, coin, coin, coin, coin)) == list(itertools.product(coin, repeat=6))
```




    True



### Compare Possible Outcomes

Flipping six two-sided coins yields $2^6 = 60$ possible outcomes and rolling two six-sided dice yields $6^2 = 36$ possible outcomes. The power of exponential growth!


```python
coin_permutations > dice_permutations
```




    True


