---
title: "Game Show Problem"
author: "Greg Barbieri"
date: 2022-04-18
description: "Optimal decision making in the Monty Hall Problem."
type: "code_tutorials"
---

The Game-Show Problem, or Monty Hall Problem according to <a href="https://en.wikipedia.org/wiki/Monty_Hall_problem"> Wikipedia</a>.

1. Choose one of three doors, one of which has the desired prize.
2. The game show host always opens one of the remaining two doors which does not have the prize behind it.
3. The host then asks the player if they would like to switch doors.
4. The player chooses whether to switch doors.
5. The host assigns a prize to the player.

What is the optimal strategy for the player?

### Import Libraries


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

### Play the Game


```python
# One door has the prize "P" and two do not have the prize "N".
doors = pd.DataFrame(data=['P','N','N'], columns=['prizes'])

runs = 100000
wins = []

for i in range(runs):
    # 1. Player selects a Door.
    doors = doors.sample(frac=1).reset_index(drop=True)
    door = doors.sample(n=1)

    # 2. Host removes a door that is neither the players door nor has the prize.
    remove = doors[(doors.index.isin(door.index) == False)
                   & (doors['prizes'] == 'N')].sample(n=1)
            
    # 3. Choose randomly whether to switch doors or not.
    switch = np.random.choice([0,1])
    
    # 4. Assign the a prize.
    if switch == 1:
        prize = doors.drop(door.index).drop(remove.index).values
    elif switch == 0:
        prize = door.values

    # 5. If door has the prize, then mark as a win.
    if prize == "P":
        wins.append([1, switch])
    else:
        wins.append([0, switch])
```

### Calculate Results

The table below shows that switching doors gives a player a 66% chance of winning while a strategy of not switching doors gives the player only a 33% chance of winning the prize.


```python
df = pd.DataFrame(data=wins, columns=['result','switch'])
```

Calculate the probability of winning if the player switches doors.


```python
df[df['switch'] == 1]['result'].sum() / df[df['switch'] == 1]['result'].count()
```




    0.669946919544343



Calculate the probability of winning if the player never switches doors.


```python
df[df['switch'] == 0]['result'].sum() / df[df['switch'] == 0]['result'].count()
```




    0.33433268275015593


