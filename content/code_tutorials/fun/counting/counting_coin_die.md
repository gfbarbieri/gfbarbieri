---
title: "Roll a Die, Flip a Coin"
author: "Greg Barbieri"
date: 2017-08-25
description: "An example in counting."
type: "code_tutorials"
--- 

This question comes from Professor David Morin's book, <a href="http://www.people.fas.harvard.edu/~djmorin/book.html">Probability For the Enthusiastic Beginner</a>, Chapter 1, page 26.

1. One person rolls two six-sided dice, and another person flips six two-sided coins. <b>Which setup has the larger number of possible outcomes</b>, assuming that the order matters?

There are two situations presented in the problem:
1. One person rolls two six-sided dice.
2. One person flips six two-sided coins.

An identical way to phrase the first situation is, one person rolls one six-sided die twice. The concept embedded in this statement is that we are dealing with identical trials (or repetition/replacement).

To paraphrase Professor Morin, if we take a ball from a box and put it back, future drawings can show a repeat of the ball drawn previously. This is inherent in rolling dice because "you don't remove the dots on a die after you roll it!" (Page 7-8).

Since repetitions are allowed and the problem states order matters, we are to use the following formula, where N represents the number of outcomes (6 on a die) and k represents the number of trials or rolls (2 in this case): $$N^{k} = 6^2 = 36$$

A fun way to solve is problem is by brute force using the itertools library. We start by importing the itertools library and creating a list called <b>die</b>, which will represent our six-sided die. You could just as easily mimic a 20-sided die by creating a list with 1-20 instead of 1-6.

# Imports

```python
import itertools

die = ['1','2','3','4','5','6']
die
```
    ['1', '2', '3', '4', '5', '6']


If you prefer the statement "rolling two six-sided die once", then you can create all possible outcomes of rolling two identical die in the following matter.

Using the <b>product()</b> function, we will perform a Cartesian product of the list <b>die</b> and itself. Each permutation will be stored in a list called <b>dice_permutations</b>.


```python
dice_permutations = list(itertools.product(die, die))
```

If you prefer the statement "rolling one six-sided die twice", then create all possible outcomes using the repeat option instead of explicitly stating the two lists.


```python
dice_permutations = list(itertools.product(die, repeat=2))
```

Both return the same outcomes, as we can see from the following comparison.


```python
list(itertools.product(die, die)) == list(itertools.product(die, repeat=2))
```

    True



The power of the itertools library allows us write out all of the outcomes associated with rolling one six-sided die twice. In other words, we can print the elements of the list <b>dice_permutations</b>, where each element is one of the possible outcomes from rolling a die twice (or two dice once).


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



By printing the length, we see that the list <b>dice_permutations</b> has 36 elements ($6^2$).


```python
len(dice_permutations)
```




    36



The second situation involves one person flipping six two-sided coins, or equivalently, one person flipping one two-sided coin six times.

Let's create a list called <b>coin</b> which will have the two outcomes of flipping a coin: 'H' for heads and 'T' for tails.


```python
coin = ['H','T']
coin
```




    ['H', 'T']



If you prefer the concept of flipping six two-sided coins, then explicitly list all six coins in the <b>product()</b> function. The following line will create a list called <b>coin_permutations</b>, where each element will have one outcome from flipping six coins simultaneously.


```python
coin_permutations = list(itertools.product(coin, coin, coin, coin, coin, coin))
```

If you prefer of flipping one two-sided coin six times, then using the repeat option will capture that conceptually.


```python
coin_permutations = list(itertools.product(coin, repeat=6))
```

The two approaches are identical, as we can see from the comparison below.


```python
list(itertools.product(coin, coin, coin, coin, coin, coin)) == list(itertools.product(coin, repeat=6))
```




    True



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



Printing the length of the list tells us that there are 64 possible outcomes of flipping a two-sided coin six times.


```python
len(coin_permutations)
```




    64



Since 64 is greater than 36 (or using our formula, $2^6$ is greater than $6^2$), flipping a two-sided coin six times produces more outcomes than rolling a six-sided die twice. Ah, the power of exponential growth!
