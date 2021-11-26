# lang.py.type.dictionary

An associative array with mapped key: value pair

## Synopsis

```py
  my_dict = ["Daniel": 13, "Jose": 25]
```

## Overview

A dictionary can contain any **inmmutable value** as it's keys. So **you can use**
[tuples](./hsr4.md) as long as they do not conatin mutalbe objects either
directly or indirectly

**Keys** must be **unique within** one **dictionary**. You can also use
[comprehension](./0loj.md) to create dictionaries

## Cookbook

### View a list of all the keys in a dictionary

You can use the `list()`, built-in function to return a list of all the keys
defined in the dictionary **in insertio order**

```py
  tel = {'jack': 4098, 'guido': 4139, 'irv': 3000}
  list(tel)         # ['jack', 'guido', 'irv']
```

- To view a sorted list of all the keys use `sorted()`

```py
  tel = {'jack': 4098, 'guido': 4139, 'irv': 3000}
  sorted(tel)       # ['guido', 'irv', 'jack']
```

### Change the value of a key

You can change the value pair of a given key by referencing it

```py
  tel = {'jack': 4098, 'sape': 4139, 'guido': 4000}
  tel["guido"] = 4127
  print(tel)        # {'jack': 4098, 'sape': 4139, 'guido': 4127}
```

### Delete a key value pair

You can delete a key and it's value with the `del` **keyword**

```py
  tel = {'jack': 4098, 'sape': 4139}
  del tel["sape"]
  print(tel)        # {'jack': 4098}
```

### Build dictionaries from sequences of key: value pairs

You can use the `dict()` built-in function to create dictionaries from key:
value pairs

```py
  tel = dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
  print(tel)        # {'sape': 4139, 'guido': 4127, 'jack': 4098}
```

### Loop through key and values at the same time

When **looping through dictionaries**, the **key and value** can be
retrieved **at the same time** using the `items()` method.

```py
  knights = {'gallahad': 'the pure', 'robin': 'the brave'}
  for k, v in knights.items():
      print(k, v)

  # gallahad the pure
  # robin the brave
```

### Loop over different lists at the same time

To **loop** over **two or more sequences** at the same time, the **entries can
be paired** with the `zip()` function.

```py
  questions = ['name', 'quest', 'favorite color']
  answers = ['lancelot', 'the holy grail', 'blue']
  for q, a in zip(questions, answers):
      print('What is your {0}?  It is {1}.'.format(q, a))

  # What is your name?  It is lancelot.
  # What is your quest?  It is the holy grail.
  # What is your favorite color?  It is blue.
```
