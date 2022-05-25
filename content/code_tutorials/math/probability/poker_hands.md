---
title: "Poker Hands"
author: "Greg Barbieri"
date: 2022-04-18
description: "Counting frequency of poker hands."
type: "code_tutorials"
---

This problem is taken directly from Professor Morin's <a href="http://www.people.fas.harvard.edu/~djmorin/book.html">Probability For the Enthusiastic Beginner</a>, Chapter 1, page 38.

> 1. In a standard 52-card deck, how many different five-card poker hands are there of each of the following types?<br>
<ol>
    <li>Full House</li>
    <li>Straight Flush</li>
    <li>Flush</li>
    <li>Straight</li>
    <li>One pair</li>
    <li>Two pairs</li>
    <li>Three of a kind</li>
    <li>Four of a kind</li>
    <li>None of the above</li>
</ol>

### Imports


```python
import itertools
import collections as col
import numpy as np
```

### Create a Deck of Cards

A deck of cards includes every unique pairing of the suits and ranks. The suits are represented by, diamonds = ‘D’, clubs = ‘C’, hearts = ‘H’, and spades = ‘S’. The ranks are represented as 2 - 10 in the usual fashion, but Jack = 11, Queen = 12, King = 13, and Ace = 14.


```python
suits = ['D','C','H','S']
ranks = [str(x) for x in range(2,15)]
```

Perform a Cartesian product of suits and ranks, yielding every ordered pair. The result will have 52 elements, which is what we expect from a standard deck of cards.


```python
deck_of_cards = list(itertools.product(ranks,suits))

len(deck_of_cards)
```




    52



### Create All 5-Card Poker Hands

Create all possible poker hands. The total number of poker hands is equal to the number of unordered 5 card arrangements, without repetitions, from 52 cards.

$$\binom{52}{5} = \frac{52!}{5!(52-5)!} = \frac{52!}{5!47!} = \frac{52 \times 51 \times 50 \times 49 \times 48}{5!} = 2,598,960$$


```python
poker_hands = list(itertools.combinations(deck_of_cards, 5))

print(format(len(poker_hands), ',d'))
```

    2,598,960


### Mathematical Example

A full house is made up of one three-of-a-kind and one two-of-a-kind. There are 13 choices (2 - Ace) for the rank appearing three times and 12 choices remaining for the rank that will appearing twice.

For the rank that appears three or two times, there are four suits. The number of ways to arrange four suits in three spots is 
$\binom{4}{3}$ and in two spots is $\binom{4}{2}$.

The total number of full house hands is equal to:

$$13 \times 12 \times \binom{4}{3} \times \binom{4}{2} = 13 \times 12 \times \frac{4!}{3!(4-3)!} \times \frac{4!}{2!(4-2)!} = 13 \times 12 \times 4 \times 6 = 3,744$$

### Find All Hands


```python
full_house = 0
one_pair = 0
two_pair = 0
straight_flush = 0
flush_only = 0
straight_only = 0
foak = 0
toak = 0
high_card = 0

for hand in poker_hands:
    ranks = []
    suits = []
    
    for rank, suit in hand:
        ranks.append(int(rank))
        suits.append(suit)
    
    ranks.sort()
    ranks_diff = np.diff(ranks)
    
    rank_count = col.Counter(ranks).most_common(2)
    suit_count = col.Counter(suits).most_common(1)
        
    if all(ranks_diff == 1) or (all(ranks_diff[:3] == 1) and ranks_diff[-1] == 9):
        hand_is_a_straight = 1
    else:
        hand_is_a_straight = 0
    
    if suit_count[0][1] == 5:
        hand_is_a_flush = 1
    else:
        hand_is_a_flush = 0

    # Full House
    if rank_count[0][1] == 3 and rank_count[1][1] == 2:
        full_house += 1
    
    # One Pair
    if rank_count[0][1] == 2 and rank_count[1][1] < 2:
        one_pair += 1
    
    # Two Pairs
    if rank_count[0][1] == 2 and rank_count[1][1] == 2:
        two_pair += 1

    # Straight-only
    if (hand_is_a_straight == 1 and hand_is_a_flush == 0):
        straight_only += 1
        
    # Flush-only
    if (hand_is_a_straight == 0 and hand_is_a_flush == 1):
        flush_only += 1
        
    # Straight Flush
    if (hand_is_a_straight == 1 and hand_is_a_flush == 1):
        straight_flush += 1

    # Four of a kind
    if rank_count[0][1] == 4:
        foak += 1
        
    # Three of a kind
    if rank_count[0][1] == 3 and rank_count[1][1] != 2:
        toak += 1
    
    # Determine high-card hand
    if rank_count[0][1] <= 1 and hand_is_a_straight == 0 and hand_is_a_flush == 0:
        high_card += 1
```


```python
print(high_card, one_pair, two_pair, flush_only, straight_only, full_house, straight_flush)
```

    1302540 1098240 123552 5108 10200 3744 40

