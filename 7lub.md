# lang.py.oper.comprehension

Embed loop logic to create data structures at their definition

## Synopsis

```py
  my_list = [<expression> for <variables> in <iterable> [<condition>]]
```

## Overview

They provide a concise way to create [list](./7cxo.md),
[dictionaries](./0loj.md) and [sets](./8u8t.md) where **each element** is the
result of **some operations** applied **to each member** of **another
sequence** or iterable

## Cookbook

### Create a list comprehension

A list comprehension is basically a `for` loop that is **expanded** and appended
**into a list**

```py
  squares = [x**2 for x in range(5)]
  print(squares)      # [0, 1, 4, 9, 16]
```

This the **same as**:

```py
  for x in range(5):
      squares.append(x**2)

  print(squares)    # [0, 1, 4, 9, 16]
```

### Create a conditional list comprehension

Just like in your `for` loop statement, you can **add a conditional** statement
inside your loop

```py
  pairs = [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
  print(pairs)

  # [(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

This the **same as**:

```py
  pairs = []

  for x in [1,2,3]:
      for y in [3,1,4]:
          if x != y:
              pairs.append((x, y))

  print(pairs)

  # [(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

### Create a dictionary comprehension

You can create a dictonary in the same way but using `{}` and specifying the
**dictonary pair**

```py
  names = ["Bruce", "Clark"]
  heros = ["Batman", "Superman"]

  my_dict = {names[i]: heros[i] for i in range(len(names))}
  print(my_dict)

  # {'Bruce': 'Batman', 'Clark': 'Superman'}
```

This the **same as**:

```py
  my_dict = {}
  for name, hero in zip(names, heros):
      my_dict[name] = hero

  print(my_dict)

  # {'Bruce': 'Batman', 'Clark': 'Superman'}
```

### Create a set comprehension

You can create a set comprehension in the same way but using `{}`

```py
  nums = [1, 1, 2, 1, 3, 4, 3, 4, 5, 5, 6, 7, 8, 7, 9, 9]

  my_set = {n for n in nums}
  print(my_set)                 # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

This the **same as**:

```py
  my_set = set()
  for n in nums:
      my_set.add(n)

  print(my_set)                 # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Create a nested list comprehension

You can **have any arbitrary expression** in your initial expression,
**including another list** comprehension

```py
  matrix = [
      [1, 2, 3, 4],
      [5, 6, 7, 8],
      [9, 10, 11, 12],
  ]

  transposed = [[row[i] for row in matrix] for i in range(4)]
  print(transposed)

  # [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

This the **same as**:

```py
  transposed = []

  for i in range(4):
      transposed.append([row[i] for row in matrix])

  print(transposed)
  # [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```
