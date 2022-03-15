---
title: "Removing Repetitions"
author: "Greg Barbieri"
date: 2017-08-26
description: "Removing repetitions, avoiding double counting."
type: "code_tutorials"
--- 

This question comes from Professor David Morin's book, <a href="http://www.people.fas.harvard.edu/~djmorin/book.html">Probability For the Enthusiastic Beginner</a>, Chapter 1, page 26.

1. We know that the number of ordered sets of three people chosen from five people is $5 \times 4 \times 3 = 60$. Reproduce this results by starting with the naive answer of $5^3 = 125$ ordered sets where repetitions are allowed, and then subtracting off the number of triplets that have repeated people.

The naive answer comes from the formula $N^{k}$, where we want to select $k$ people from $N$ people, hence $5^3 = 125$. The answer without repetitions comes from the following formula: $$\frac{N!}{(N-k)!} = \frac{5!}{(5-3)!} = \frac{5!}{2!} = 5 \times 4 \times 3 = 60$$

Using Python, we will count, search for, and remove the repetitions!

Let's import the required libraries and create a list called <b>people</b> with five elements, each distinctly representing one of the five people.


```python
import itertools
import pandas as pd

people = ['P1', 'P2', 'P3', 'P4', 'P5']
```

To get the naive answer of $5^3 = 125$ ordered sets of three people, we will use the <b>product()</b> function from the itertools library. We will store them in the list called <b>perm_w_rep</b>.


```python
perm_w_rep = list(itertools.product(people, repeat=3))
len(perm_w_rep)
```




    125



If an arrangement contains a person (P1 - P5) more than once, then that arrangement is said to have a repetition. Before we search for and remove arrangements with repetitions, let's write out a few examples.

The first type of arrangement with repetitions is when the same person is selected to fill all three spots. This can only occur one way for each person. Since there are five people, there are five arrangements with repetitions of this type of in our list <b>perm_w_rep</b>. All five are written out below.


```python
print(perm_w_rep[0], perm_w_rep[31], perm_w_rep[62], perm_w_rep[93], perm_w_rep[124])
```

    ('P1', 'P1', 'P1') ('P2', 'P2', 'P2') ('P3', 'P3', 'P3') ('P4', 'P4', 'P4') ('P5', 'P5', 'P5')


The second type of arrangement with repetitions is when one person is selected twice, with a different person selected only once to fill the remaining spot. This type of arrangement can arise in three different ways for any two people. Below are the three different ways P1 can be selected twice and P2 selected once.


```python
print(perm_w_rep[1], perm_w_rep[5], perm_w_rep[25])
```

    ('P1', 'P1', 'P2') ('P1', 'P2', 'P1') ('P2', 'P1', 'P1')


My first instinct to search the list <b>perm_w_rep</b> for arrangements with repetitions is to throw all the arrangements in a Pandas DataFrame. Each arrangement would be a row and each position in the arrangement would be the column value.

Create the DataFrame <b>df_perm_w_rep</b>, naming the columns after the position of the person in the arrangement.


```python
df_perm_w_rep = pd.DataFrame(perm_w_rep, columns = ['First', 'Second', 'Third'])
df_perm_w_rep.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>First</th>
      <th>Second</th>
      <th>Third</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>P1</td>
      <td>P1</td>
      <td>P1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>P1</td>
      <td>P1</td>
      <td>P2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>P1</td>
      <td>P1</td>
      <td>P3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>P1</td>
      <td>P1</td>
      <td>P4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>P1</td>
      <td>P1</td>
      <td>P5</td>
    </tr>
  </tbody>
</table>
</div>



If the value of First equals the value of Second, on the same row, then that arrangement has repetitions. The same logic applies if the value of Second equals the value of Third or the value for First equals Third.

We will use this logic to set a variable called <b>Repetitions</b> to either True or False. If any of the three positions (three columns) in the arrangement are equal, then that arrangement has a repeated person, setting the variable <b>Repetitions</b> to True.


```python
df_perm_w_rep['Repetitions'] = ((df_perm_w_rep['First'] == df_perm_w_rep['Second']) | 
                                (df_perm_w_rep['First'] == df_perm_w_rep['Third']) | 
                                (df_perm_w_rep['Second'] == df_perm_w_rep['Third']))
df_perm_w_rep.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>First</th>
      <th>Second</th>
      <th>Third</th>
      <th>Repetitions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>P1</td>
      <td>P1</td>
      <td>P1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>P1</td>
      <td>P1</td>
      <td>P2</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>P1</td>
      <td>P1</td>
      <td>P3</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>P1</td>
      <td>P1</td>
      <td>P4</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>P1</td>
      <td>P1</td>
      <td>P5</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



Counting the values of the variable <b>Repetitions</b> (either True or False) will tell us exactly how many arrangements have a repeated person. The results show that there are 65 arrangements with repetitions and 60 without.


```python
df_perm_w_rep['Repetitions'].value_counts()
```




    True     65
    False    60
    Name: Repetitions, dtype: int64



To remove the repetitions, we can create a new DataFrame <b>df_perm_wo_rep</b> with only rows where the variable <b>Repetitions</b> is equal to False. We then clean up the DataFrame by dropping the variable <b>Repetitions</b>.


```python
df_perm_wo_rep = df_perm_w_rep[df_perm_w_rep['Repetitions'] == False].drop('Repetitions', axis=1)
```

A count of the number of rows in our new DataFrame <b>df_perm_wo_rep</b> shows we have 60 arrangements remaining. This is what we would expect from the formula without repetitions.


```python
len(df_perm_wo_rep)
```




    60



Personally, I don't feel complete unless we leave our list in the way that we found it. Let's convert the DataFrame back to a list of tuples.


```python
perm_wo_rep = []
for element in df_perm_wo_rep.to_records(index=False):
    perm_wo_rep.append(tuple(element))

len(perm_wo_rep)
```




    60


