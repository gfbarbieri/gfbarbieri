---
title: "Roll a Die, Flip a Coin"
author: "Greg Barbieri"
date: 2017-08-25
description: "Counting possible outcomes."
type: "code_tutorials"
--- 

This question comes from Professor David Morin's book, <a href="http://www.people.fas.harvard.edu/~djmorin/book.html">Probability For the Enthusiastic Beginner</a>, Chapter 1, page 26.

1. One person rolls two six-sided dice, and another person flips six two-sided coins. <b>Which setup has the larger number of possible outcomes</b>, assuming that the order matters?

Import the itertools library and create a list called which will represent a six-sided die. You could easily mimic a 20-sided die by creating a list with 1-20 instead of 1-6.

# Imports

```python
import itertools

die = ['1','2','3','4','5','6']
die
```
    ['1', '2', '3', '4', '5', '6']


If you prefer the statement "rolling two six-sided die once", then you can create all possible outcomes of rolling two identical die using the <b>product</b> function, returning a Cartesian product of the list <b>die</b> and itself.


```python
dice_permutations = list(itertools.product(die, die))
```

If you prefer the equivalent statement "rolling one six-sided die twice", then create all possible outcomes using the repeat option instead of explicitly stating the two lists.


```python
dice_permutations = list(itertools.product(die, repeat=2))
```

Both return the same outcomes, as we can see from the following comparison.


```python
list(itertools.product(die, die)) == list(itertools.product(die, repeat=2))
```

    True


The list <b>dice_permutations</b> has 36 elements ($6^2$).


```python
len(dice_permutations)
```




    36


Print the elements of the list, where each element is one of the possible outcomes from rolling a die twice (or two dice once).


```python
dice_permutations
```

    [('1', '1'),
     ('1', '2'),
     ('1', '3'),
     ('1', '4'),
     ('1', '5'),
     ('1', '6'),
     ('2', '1'),
     ('2', '2'),
     ('2', '3'),
     ('2', '4'),
     ('2', '5'),
     ('2', '6'),
     ('3', '1'),
     ('3', '2'),
     ('3', '3'),
     ('3', '4'),
     ('3', '5'),
     ('3', '6'),
     ('4', '1'),
     ('4', '2'),
     ('4', '3'),
     ('4', '4'),
     ('4', '5'),
     ('4', '6'),
     ('5', '1'),
     ('5', '2'),
     ('5', '3'),
     ('5', '4'),
     ('5', '5'),
     ('5', '6'),
     ('6', '1'),
     ('6', '2'),
     ('6', '3'),
     ('6', '4'),
     ('6', '5'),
     ('6', '6')]



The second situation involves one person flipping six two-sided coins, or equivalently, one person flipping one two-sided coin six times.

Let's create a list representing the two outcomes of flipping a coin.


```python
coin = ['H','T']
coin
```




    ['H', 'T']



If you prefer flipping six two-sided coins, then use the <b>product</b> again to create every combination of the six coins.


```python
coin_permutations = list(itertools.product(coin, coin, coin, coin, coin, coin))
```

If you prefer of flipping one two-sided coin six times, then using the repeat option.


```python
coin_permutations = list(itertools.product(coin, repeat=6))
```

Again, the two approaches are identical.

```python
list(itertools.product(coin, coin, coin, coin, coin, coin)) == list(itertools.product(coin, repeat=6))
```




    True


There are 64 possible outcomes of flipping a two-sided coin six times.


```python
len(coin_permutations)
```




    64


We can write out our sample space from flipping six coins to see what it looks like.


```python
coin_permutations
```




    [('H', 'H', 'H', 'H', 'H', 'H'),
     ('H', 'H', 'H', 'H', 'H', 'T'),
     ('H', 'H', 'H', 'H', 'T', 'H'),
     ('H', 'H', 'H', 'H', 'T', 'T'),
     ('H', 'H', 'H', 'T', 'H', 'H'),
     ('H', 'H', 'H', 'T', 'H', 'T'),
     ('H', 'H', 'H', 'T', 'T', 'H'),
     ('H', 'H', 'H', 'T', 'T', 'T'),
     ('H', 'H', 'T', 'H', 'H', 'H'),
     ('H', 'H', 'T', 'H', 'H', 'T'),
     ('H', 'H', 'T', 'H', 'T', 'H'),
     ('H', 'H', 'T', 'H', 'T', 'T'),
     ('H', 'H', 'T', 'T', 'H', 'H'),
     ('H', 'H', 'T', 'T', 'H', 'T'),
     ('H', 'H', 'T', 'T', 'T', 'H'),
     ('H', 'H', 'T', 'T', 'T', 'T'),
     ('H', 'T', 'H', 'H', 'H', 'H'),
     ('H', 'T', 'H', 'H', 'H', 'T'),
     ('H', 'T', 'H', 'H', 'T', 'H'),
     ('H', 'T', 'H', 'H', 'T', 'T'),
     ('H', 'T', 'H', 'T', 'H', 'H'),
     ('H', 'T', 'H', 'T', 'H', 'T'),
     ('H', 'T', 'H', 'T', 'T', 'H'),
     ('H', 'T', 'H', 'T', 'T', 'T'),
     ('H', 'T', 'T', 'H', 'H', 'H'),
     ('H', 'T', 'T', 'H', 'H', 'T'),
     ('H', 'T', 'T', 'H', 'T', 'H'),
     ('H', 'T', 'T', 'H', 'T', 'T'),
     ('H', 'T', 'T', 'T', 'H', 'H'),
     ('H', 'T', 'T', 'T', 'H', 'T'),
     ('H', 'T', 'T', 'T', 'T', 'H'),
     ('H', 'T', 'T', 'T', 'T', 'T'),
     ('T', 'H', 'H', 'H', 'H', 'H'),
     ('T', 'H', 'H', 'H', 'H', 'T'),
     ('T', 'H', 'H', 'H', 'T', 'H'),
     ('T', 'H', 'H', 'H', 'T', 'T'),
     ('T', 'H', 'H', 'T', 'H', 'H'),
     ('T', 'H', 'H', 'T', 'H', 'T'),
     ('T', 'H', 'H', 'T', 'T', 'H'),
     ('T', 'H', 'H', 'T', 'T', 'T'),
     ('T', 'H', 'T', 'H', 'H', 'H'),
     ('T', 'H', 'T', 'H', 'H', 'T'),
     ('T', 'H', 'T', 'H', 'T', 'H'),
     ('T', 'H', 'T', 'H', 'T', 'T'),
     ('T', 'H', 'T', 'T', 'H', 'H'),
     ('T', 'H', 'T', 'T', 'H', 'T'),
     ('T', 'H', 'T', 'T', 'T', 'H'),
     ('T', 'H', 'T', 'T', 'T', 'T'),
     ('T', 'T', 'H', 'H', 'H', 'H'),
     ('T', 'T', 'H', 'H', 'H', 'T'),
     ('T', 'T', 'H', 'H', 'T', 'H'),
     ('T', 'T', 'H', 'H', 'T', 'T'),
     ('T', 'T', 'H', 'T', 'H', 'H'),
     ('T', 'T', 'H', 'T', 'H', 'T'),
     ('T', 'T', 'H', 'T', 'T', 'H'),
     ('T', 'T', 'H', 'T', 'T', 'T'),
     ('T', 'T', 'T', 'H', 'H', 'H'),
     ('T', 'T', 'T', 'H', 'H', 'T'),
     ('T', 'T', 'T', 'H', 'T', 'H'),
     ('T', 'T', 'T', 'H', 'T', 'T'),
     ('T', 'T', 'T', 'T', 'H', 'H'),
     ('T', 'T', 'T', 'T', 'H', 'T'),
     ('T', 'T', 'T', 'T', 'T', 'H'),
     ('T', 'T', 'T', 'T', 'T', 'T')]


Since 64 is greater than 36 ($2^6 > 6^2$), flipping a two-sided coin six times produces more outcomes than rolling a six-sided die twice. Ah, the power of exponential growth!