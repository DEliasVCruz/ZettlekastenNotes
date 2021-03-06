# lang.py.data.dictionary

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
defined in the dictionary **in inserti order**

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

### Create a dictionary with iterable keys

**Normally** you **wouldn't** be able to pass an **iterable as the key** of a dictionary,
other than [strings](./4t3v.md), since they **keys have to be inmutable** and list
an other iterables tend to be mutable

You can use [frozensets](./8u8t.md) to pass a set, an iterable, as the key of a
dictionary

```py
  key_1 = frozenset([1, 2])
  key_2 = frozenset([3, 4])

  my_dict = {key_1: 'good', key_2: 'bad'}
  pairs = []

  for key, value in my_dict.items():
      for element in key:
          pairs.append((element, value))

# [(1, 'good'), (2, 'good'), (3, 'bad'), (4, 'bad')]
```

### Build dictionaries from sequences of key: value pairs

You can use the `dict()` built-in function to create dictionaries from key:
value pairs

```py
  tel = dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
  print(tel)        # {'sape': 4139, 'guido': 4127, 'jack': 4098}
```

### Build a dictionary from two lists

Following the same process from the past recipe we can *use* the `zip()`
**function** **to build** the **list of** `key: value` **pairs** from two
separete lists

```py
  names = ["Daniel", "Jose"]
  ages = [23, 22]
  my_dict = dict(zip(names, ages))
  print(my_dict)                    # {'Daniel': 23, 'Jose': 22}
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

### Loop over the keys of a dictionary

The **default** way of looping over a dictionary is doing it **by it's keys**

```py
  for key in my_dict:
      print(key)
```

### Get a list of the the values

You can get a list of all the values in your dictionary with the `values()`
method

```py
  for value in my_dict.values():
      print(value)
```
