---
title: "Counting Poker Hands"
author: "Greg Barbieri"
date: 2017-09-23
description: "How to count poker hands using Python."
type: "code_tutorials"
--- 

This problem is taken directly from Professor Morin's <a href="http://www.people.fas.harvard.edu/~djmorin/book.html">Probability For the Enthusiastic Beginner</a>, Chapter 1, page 38.

1. In a standard 52-card deck, how many different five-card poker hands are there of each of the following types?<br>
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

For each type, it is understood that we don't count hands that also fall into a higher category. For example, when counting the three-of-a-kind hands, we <i>don't</i> count the full-house or four-of-a-kind hands, even though they technically contain three cards of the same kind. 

In case it isn't obvious, a standard deck has four suits and each suit has thirteen ranks. In the U.S., poker involves assessing the outcome of five cards. The ace is the highest rank (but can also represent one), the two is the lowest rank (when ace isn't), and there is no hierarchy among the suits.

## Part 1: Creating a Deck of Cards

Before we can count any poker hands, we need to create a deck of cards.

A deck of cards includes every unique pairing of the suits and ranks. The suits will be stored in a list <b>suits</b> and are represented by, diamonds = 'D', clubs = 'C', hearts = 'H', and spades = 'S'. The ranks will be stored in a list <b>ranks</b>, where ranks 2 - 9 are represented in the usual fashion, but 10 = 'T', Jack = 'J', Queen = 'Q', King = 'K', and Ace = 'A'.


```python
suits = 'DCHS'
ranks = '23456789TJQKA'
```

The itertools library has a function called <b>product()</b>, which we will use to perform a Cartesian product of <b>suits</b> and <b>ranks</b>, yielding every ordered pair. The resulting list <b>cards</b> will have 52 elements, which is what we expect from a standard deck of cards.


```python
import itertools

cards = list(itertools.product(ranks,suits))
len(cards)
```




    52



#### A Visually Appealing Deck of Cards

Printing the first five cards in our deck shows that they are in the format ('R','S'), where the first element in the tuple is the rank and the second is the suit. I have never asked someone to give me a dataset representing playing cards before, but if I did, I would expect it in the more visually pleasing format 'RS'.
cards[:5]
Converting each card from the format ('R','S') to 'RS' will be done using the <b>join()</b> function. In our case, we want to join each element in the tuple together, without any characters in between. Let's show an example of the <b>join()</b> function using the two of diamonds.


```python
print(cards[0], "-->", ''.join(cards[0]))
```

    ('2', 'D') --> 2D


Perfect! Note that a single tuple is represented without parentheses, returning simply 'RS'.

Lets perform the same manipulation, but to every card in the list <b>cards</b>. Starting with an empty list called <b>deck_of_cards</b>, for each element in the list <b>cards</b>, join the rank and the suit as shown above and append it to the list <b>deck_of_cards</b>. Printing the length of the list <b>deck_of_cards</b> suggests that we have retained all 52 cards and the first five elements show it is in my desired format.


```python
deck_of_cards = []

for card in cards:
    deck_of_cards.append(''.join(card))

print(len(deck_of_cards), "-->", deck_of_cards[:5])
```

    52 --> ['2D', '2C', '2H', '2S', '3D']


It is worth mentioning here that the manipulation we performed above--iterating over a list in order to apply a function--is so common an activity that there is a built in Python function that performs it without explicit stating the for-loop. The function is called <b>map()</b>.

Let's quickly recreate the deck of cards using the <b>map()</b> function instead, but call the list <b>deck_of_cards_map</b> and compare it to <b>deck_of_cards</b>. The result of the comparisons shows that both routes return the same list.


```python
deck_of_cards_map = list(map(''.join, cards))

deck_of_cards == deck_of_cards_map
```




    True



## Part 2: Creating 5-Card Poker Hands

Now that we have a deck of cards, we can create all possible poker hands. A poker hand does not allow repetitions (depleting trails) since a card that is dealt is not put back into the deck. In addition, order doesn't matter since the five-card hand (2D, 2C, 2H, 2S, 3D) is an equivalent four-of-a-kind to (3D, 2S, 2H, 2D, 2C). Therefore, the total number of poker hands is equal to the number of unordered 5 card arrangements, without repetitions, from 52 cards.

$$\binom{52}{5} = \frac{52!}{5!(52-5)!} = \frac{52!}{5!47!} = \frac{52 \times 51 \times 50 \times 49 \times 48}{5!} = 2,598,960$$

The itertools library has a function <b>combinations</b>, which we will use to create all possible arrangements of 5 cards from 52 and store in a list called <b>poker_hands</b>. Printing the length of the list <b>poker_hands</b> suggests we have all of our expected 2,598,960 hands.


```python
poker_hands = list(itertools.combinations(deck_of_cards, 5))

print(format(len(poker_hands), ',d'))
```

    2,598,960


For something tangible, below a random selection of 50 poker hands.


```python
import random

random.sample(poker_hands, 50)
```




    [('3H', '7C', '7H', '8S', 'AC'),
     ('5S', '6D', 'JD', 'QS', 'AC'),
     ('3H', '5C', '7S', '9H', 'TS'),
     ('5H', '9H', 'JH', 'QD', 'AC'),
     ('6D', 'TD', 'JS', 'QH', 'QS'),
     ('3C', '4H', '8H', 'TH', 'JH'),
     ('3C', '5S', '7S', 'KD', 'KH'),
     ('4C', '4H', '6D', '8C', 'KH'),
     ('2H', '9S', 'TD', 'TC', 'JC'),
     ('4C', '4H', '6C', '6H', 'AD'),
     ('2S', '5D', '8D', 'TD', 'JH'),
     ('5H', '6C', '7H', '8C', 'TS'),
     ('7H', '9C', 'JH', 'AD', 'AH'),
     ('2D', '2S', '3C', '5D', '7H'),
     ('2S', '4S', '6H', '9S', 'AS'),
     ('4H', '6H', '7H', '8S', '9H'),
     ('3D', '8S', '9S', 'TC', 'AD'),
     ('3D', '4C', '8D', '9C', 'JC'),
     ('2D', '7S', 'TD', 'JC', 'JS'),
     ('5S', '7C', '7S', '9D', 'JS'),
     ('2S', '4H', '7C', '8H', 'QC'),
     ('2C', '2S', '4C', 'KS', 'AC'),
     ('2H', '3C', '5D', 'JH', 'AS'),
     ('5S', '6C', '9C', '9S', 'TD'),
     ('3C', '4H', '5S', '8C', 'AD'),
     ('2D', '4D', '4H', '7H', '8D'),
     ('2S', '4S', '8H', 'QD', 'KD'),
     ('3S', '7H', 'TH', 'QC', 'KD'),
     ('4D', '5S', '7D', 'JC', 'QC'),
     ('2C', '4C', '7H', '8D', '8C'),
     ('2C', '7S', 'KD', 'KC', 'AD'),
     ('4D', '8H', 'JC', 'KD', 'KH'),
     ('2C', 'TD', 'TC', 'KC', 'KS'),
     ('2S', '5D', '7H', '8C', 'JC'),
     ('4D', '4H', '6S', 'KH', 'AD'),
     ('4S', '8S', '9S', 'KS', 'AC'),
     ('2S', '8C', 'JH', 'KH', 'AH'),
     ('3D', '6S', '9S', 'TH', 'JC'),
     ('4D', '6C', '6H', '6S', 'JS'),
     ('4S', '6D', 'TH', 'QH', 'AS'),
     ('5D', '6S', '8H', '8S', 'QH'),
     ('5S', '8D', 'JH', 'QD', 'QS'),
     ('3H', 'TS', 'QC', 'KH', 'AC'),
     ('9D', 'TC', 'JH', 'KC', 'AC'),
     ('3C', '4S', 'TC', 'KS', 'AS'),
     ('2C', '4D', '4C', '5H', '8D'),
     ('2D', '2H', '3D', '5C', '8C'),
     ('TH', 'JC', 'QC', 'QH', 'KD'),
     ('9S', 'QS', 'KD', 'KS', 'AC'),
     ('2C', '4C', '6C', '8S', 'TS')]



## Part 3: Counting Poker Hands

Since poker hands are combinations of repeated ranks and suits (three repetitions of one rank, five repetitions of one suit, etc.), my main tool will be the <b>Counter()</b> function (or is it a module) in the <b>collections</b> library. The process gets repetitive, so I do most of the explaining when counting the first four hands.

Let's import the libraries needed and get counting!


```python
import collections as col
import numpy as np
```

### A. Full House

#### The Math

A full house is made up of one three-of-a-kind and one pair (two of a kind). There are 13 choices (2 - Ace) for the rank that will appear 3 times. After, there will be 12 remaining choices (13 minus 1) for the rank that will appear 2 times.

For the rank that is selected to appear 3 times, there are 4 suits available. The number of ways to arrange 4 suits in 3 spots is $\binom{4}{3}$. Similarly, there are 4 suits available for the rank that is selected to appear twice, with $\binom{4}{2}$ possible arrangements of the suits.

Putting it all together, the total number of full house hands is equal to:

$$13 \times 12 \times \binom{4}{3} \times \binom{4}{2} = 13 \times 12 \times \frac{4!}{3!(4-3)!} \times \frac{4!}{2!(4-2)!} = 13 \times 12 \times 4 \times 6 = 3,744$$

#### The Process

<ol>
<li>
We will set a variable called <b>full_house</b> to zero and we will use it to count the number of full house hands.
</li>

<li>
A full house is made up of one rank repeated three times and another repeated twice, requiring us to only assess the ranks. We will do this by looping over each hand in the list <b>poker_hands</b> and assessing its ranks.
</li>

<li>
For each card in the hand, append the rank (the first element of the card in format 'RS') to the list <b>ranks_in_hand</b>.
</li>

<li>
Once we have all five ranks stored, we want to count the frequency of the ranks in <b>ranks_in_hand</b> and store the two most common ranks in a list called <b>rank_count</b>.
</li>

<li>
If the most common rank is repeated 3 times, there is certainly a three-of-a-kind in the hand. If the second most common rank is repeated twice, then there is a pair. If both conditions are true, then the hand is a full house!
</li>


```python
#1.
full_house = 0

#2.
for hand in poker_hands:
    ranks_in_hand = []
    
    #3.
    for rank_of_card, suit_of_card in hand:
        ranks_in_hand.append(rank_of_card)
    
    #4.
    rank_count = col.Counter(ranks_in_hand).most_common(2)
    
    #5.
    if rank_count[0][1] == 3 and rank_count[1][1] == 2:
        full_house += 1
```

Printing the variable <b>full_house</b> returns 3,744, suggesting we counted correctly.


```python
print(format(full_house, ',d'))
```

    3,744


### B. Straight Flush, C. Straight-Only, D. Flush-Only 

The process for counting flush-only, straight-only, and straight flush hands is so similar that I will not repeat it separately and will show all three together.

#### The Process
1. Set three variables <b>straight_flush</b>, <b>flush_only</b>, <b>straight_only</b> to zero. These will be our counters.

2. A straight flush requires that we assess both ranks and suits. We will use the ranks to determine a straight and the suits to determine a flush. We will loop over every poker hand as we did to count full house hands.

3. For each hand in our list <b>poker_hands</b>, create two empty lists to store the ranks and suits of each five-card hand. I represented 10 - Ace alphabetically, but I will need them represented numerically for determining a straight. Then for each card in the hand, append the suit and rank to <b>suits_in_hand</b> and <b>ranks_in_hand</b>, respectively.

4. Sort the ranks from low to high. Take the lagged difference of the elements in <b>ranks_in_hand</b> using the <b>diff()</b> function from the <b>numpy</b> library and store it in <b>rank_lag_dff</b>. 

5. Using Python's built-in function <b>all()</b>, we can determine if the difference between all the elements are 1. If true, then the hand is a straight. The only exception is the hand ('A','2','3','4','5') which will appear as ('2','3','4','5','14'). In that case, the last element of <b>rank_lag_diff</b> can be 9 as well as 1.

6. Produce the frequencies of the suits in each hand stored in <b>suits_in_hand</b>. If a suit is repeated 5 times, then the entire hand has only one suit and the hand is a flush.

At this point, we can set the conditions for a straight-only, flush-only, and straight flush. If the hand is a straight and not a flush, then the hand is a straight-only and vice versa for the flush-only. If both conditions are satisfied, it is a straight flush.


```python
#1.
straight_flush = 0
flush_only = 0
straight_only = 0

#2.
for hand in poker_hands:
    ranks_in_hand = []
    suits_in_hand = []
    
    #3.
    for rank_of_card, suit_of_card in hand:
        if rank_of_card == 'T':
            rank_of_card = 10
        elif rank_of_card == 'J':
            rank_of_card = 11
        elif rank_of_card == 'Q':
            rank_of_card = 12
        elif rank_of_card == 'K':
            rank_of_card = 13
        elif rank_of_card == 'A':
            rank_of_card = 14

        ranks_in_hand.append(int(rank_of_card))
        suits_in_hand.append(suit_of_card)
    
    #4.
    ranks_in_hand.sort()
    ranks_lag_diff = np.diff(ranks_in_hand)

    #5.
    if all(ranks_lag_diff == 1) or (all(ranks_lag_diff[:3] == 1) and ranks_lag_diff[-1] == 9):
        hand_is_a_straight = 1
    else:
        hand_is_a_straight = 0
    
    #6.
    suit_count = col.Counter(suits_in_hand).most_common(1)
    
    if suit_count[0][1] == 5:
        hand_is_a_flush = 1
    else:
        hand_is_a_flush = 0

    #Straight-only
    if (hand_is_a_straight == 1 and hand_is_a_flush == 0):
        straight_only += 1
        
    #Flush-only
    if (hand_is_a_straight == 0 and hand_is_a_flush == 1):
        flush_only += 1
        
    #Straight Flush
    if (hand_is_a_straight == 1 and hand_is_a_flush == 1):
        straight_flush += 1
```

Print the results for each hand.


```python
print("Out of %s number of poker hands, %d are a straight-only, %d are a flush-only, and %d are a straight flush." \
      % (len(poker_hands), straight_only, flush_only, straight_flush))
```

    Out of 2598960 number of poker hands, 10200 are a straight-only, 5108 are a flush-only, and 40 are a straight flush.


### E. One Pair, F. Two Pairs

Counting one and two pairs is straight forward at this point. 

1. Append all the ranks to <b>ranks_in_hand</b>.
2. Count the two most commonly occuring ranks and store them in <b>rank_count</b>. 

For one pair, if the most common rank is 2, then we know there is at least one pair. If the next most common rank is less than two the remaining cards are not repeated. If both conditions are satisfied, then there is only one pair in the hand.

Similarly for two pairs, if the two most commonly repeated ranks both equal 2, then there are two unique pairs of ranks in the hand.


```python
one_pair = 0
two_pair = 0

#1.
for hand in poker_hands:
    ranks_in_hand = []

    for rank, suit in hand:
        ranks_in_hand.append(rank)
    
    #2.
    rank_count = col.Counter(ranks_in_hand).most_common(2)
    
    #One Pair
    if rank_count[0][1] == 2 and rank_count[1][1] < 2:
        one_pair += 1
    
    #Two Pairs
    if rank_count[0][1] == 2 and rank_count[1][1] == 2:
        two_pair += 1
```

Printing the results suggest we counted correctly.


```python
print(one_pair, two_pair)
```

    1098240 123552


### G. Four of a Kind, H. Three of a Kind


1. Append all the ranks to <b>ranks_in_hand</b>.
2. Count the two most commonly occuring ranks and store them in <b>rank_count</b>. 

For four of a kind, if the most commonly repeated rank is repeated 4 times, then the hand is a four-of-a-kind.

For three of a kind, if the most commonly repeated rank is repeated 3 times and no other rank is repeated more than once (ruling our a full house), then the hand is a three-of-a-kind.


```python
foak = 0
toak = 0

#1.
for hand in poker_hands:
    ranks_in_hand = []
    
    #2.
    for rank, suit in hand:
        ranks_in_hand.append(rank)
    
    rank_count = col.Counter(ranks_in_hand).most_common(2)
    
    #Four of a kind
    if rank_count[0][1] == 4:
        foak += 1

    #Three of a kind
    if rank_count[0][1] == 3 and rank_count[1][1] != 2:
        toak += 1
```


```python
print(foak, toak)
```

    624 54912


### I. None of the Above (High-card)

The basis for counting high card hands is that all ranks must appear only once. However, that conditions also applies to a straight, so we have to rule those out. Finally, we need to make sure a hand does not have five of the same suits, otherwise its a flush! In total, counting high-card hands is almost identical to what we did for a straight flush.

1. Append all the ranks and suits to <b>ranks_in_hand</b> and <b>suits_in_hand</b>.
2. Count the two most commonly occuring ranks and suits and store them in <b>rank_count</b>, <b>suit_count</b>, respectively.
3. If the most commonly repeated rank is only repeated 1 time, then all the ranks are unique in the hand. This is the first condition for determining a high-card hand.
4. Determine whether the hand is a straight.
5. Determine whether the hand is a flush.
6. If the hand has no repeated ranks, is not a straight, and is not a flush, its a high-card hand.


```python
high_card = 0

#1.
for hand in poker_hands:
    ranks_in_hand = []
    suits_in_hand = []
    
    for rank_of_card, suit_of_card in hand:
        if rank_of_card == 'T':
            rank_of_card = 10
        elif rank_of_card == 'J':
            rank_of_card = 11
        elif rank_of_card == 'Q':
            rank_of_card = 12
        elif rank_of_card == 'K':
            rank_of_card = 13
        elif rank_of_card == 'A':
            rank_of_card = 14

        ranks_in_hand.append(int(rank_of_card))
        suits_in_hand.append(suit_of_card)
    
    #2.
    rank_count = col.Counter(ranks_in_hand).most_common(1)
    suit_count = col.Counter(suits_in_hand).most_common(1)
    
    #3. Unique ranks, no repeats
    if rank_count[0][1] > 1:
        repeated_ranks = 1
    else:
        repeated_ranks = 0
    
    #4. Rule out straight
    ranks_in_hand.sort()
    ranks_lag_diff = np.diff(ranks_in_hand)

    if all(ranks_lag_diff == 1) or (all(ranks_lag_diff[:3] == 1) and ranks_lag_diff[-1] == 9):
        hand_is_a_straight = 1
    else:
        hand_is_a_straight = 0
    
    #5. Rule out flush
    if suit_count[0][1] == 5:
        hand_is_a_flush = 1
    else:
        hand_is_a_flush = 0
    
    #6. Determine high-card hand
    if repeated_ranks == 0 and hand_is_a_straight == 0 and hand_is_a_flush == 0:
        high_card += 1
```

Print the number of high-card hands. We see that about 50% percent of all poker hands are high-card hands.


```python
print(high_card, high_card / len(poker_hands))
```

    1302540 0.5011773940345369

