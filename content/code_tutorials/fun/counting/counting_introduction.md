---
title: "Counting, an Introduction"
author: "Greg Barbieri"
date: 2017-08-17
description: "An introduction to approaching counting problems using Python."
type: "code_tutorials"
--- 

This introductory question comes directly from <a href="http://www.people.fas.harvard.edu/~djmorin/book.html">Probability For the Enthusiastic Beginner</a>, Chapter 1, page 26.

1. Six girls and four boys are to be assigned to ten seats in a row, with the stipulations that a girl sits in the third seat and a boy sits in the eighth seat. <b>How many arrangements are possible?</b>

If we ignore the stipulations for a moment, then the question becomes “how many arrangements of 10 people (6 girls + 4 boys) are possible?"

Since we are dealing with people, we can safely assume no replacement, and in this particular case, order matters. According to Table 1.10 on page 22, the proper equation to use is:

$$\frac{N!}{(N-n)!} = \frac{10!}{(10-10)!} = 10! = 3,628,800$$

## Imports

The itertools library has a function called <b>permutations()</b>, which we will use to generate all of the ordered arrangements without stipulations.


```python
import math
import itertools
```

The number of arrangements that satisfy the stipulations will be a subset of the 3,628,800 arrangements without the stipulations. All we need to do is find them!

Let's create a list called <b>lst</b>, consisting of six girls and four boys. We will use the list to generate all possible arrangements.


```python
lst = ['G', 'G', 'G', 'G', 'G', 'G', 'B', 'B', 'B', 'B']
lst
```




    ['G', 'G', 'G', 'G', 'G', 'G', 'B', 'B', 'B', 'B']



Let's store the arrangements in a list called <b>all_arrangements</b>. The length of our list confirms the expected number of arrangements.


```python
all_arrangements = list(itertools.permutations(lst, 10))

len(all_arrangements)
```




    3628800



One arrangement of the six girls and four boys is:


```python
all_arrangements[100]
```




    ('G', 'G', 'G', 'G', 'G', 'B', 'G', 'B', 'B', 'B')



Another arrangement is:


```python
all_arrangements[1000]
```




    ('G', 'G', 'G', 'G', 'B', 'G', 'B', 'B', 'G', 'B')



Let's start with the stipulation that a boy sit in the eighth seat. We can count the number of arrangements that satisfy the stipulation by iterating over each of the elements in the list <b>all_arrangements</b> using a for-loop. 

At each iteration, we will use an if-statement to check whether the 8th element of the arrangement is a “B”. If the condition is true, then increment the counter <b>eighth_seat_boy</b> by one.


```python
eighth_seat_boy = 0

for arrangement in all_arrangements:
    if arrangement[8] == "B":
        eighth_seat_boy += 1
```

Printing the counter shows that there are 1,451,520 arrangements with a boy in the eighth seat.


```python
eighth_seat_boy
```




    1451520



While a counter is more appropriate for this exercise, admittedly it was not my original approach. As a data analyst, it is common to want to perform another layer of analysis with the rows that meet the stipulations. That is, I usually need to create a separate dataset with only the rows that meet our conditions (more on that in later posts).

While premature, let's show an example of this approach when counting the number of arrangements that meet the stipulation of a girl in the third seat. Instead of incrementing a counter, each arrangement that satisfies the stipulation will be appended to the list <b>third_seat_girl</b>.


```python
third_seat_girl = []

for arrangement in all_arrangements:
    if arrangement[3] == "G":
        third_seat_girl.append(arrangement)
```

Printing the length of the list <b>third_seat_girl</b> tells us that there are 2,177,280 arrangements with a girl in the third seat.


```python
len(third_seat_girl)
```




    2177280



Lets complete the exercise by putting the two stipulations together and counting the number of arrangements.


```python
both_stipulations = 0

for arrangement in all_arrangements:
    if arrangement[3] == "G" and arrangement[8] == "B":
        both_stipulations += 1
```

Printing the counter <b>both_stipulations</b> shows 967,680 arrangements with a girl in the third seat and a boy in the eighth seat. This is in fact the answer to the problem!


```python
both_stipulations
```




    967680


