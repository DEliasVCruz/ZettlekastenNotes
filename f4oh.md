# lang.py.module.random

Built-in module to generate pseudo-random elements

## Synopsis

```py
  import random
```

## Overview

You can use this module to generate random numbers in various ways, though is
not **true randmoness** for **criptograpich** needs you should use the
**built-in** [secrets](./6vbi.md) module instead

## Cookbook

### Generate a random float

You can generate a **random float between 0.0 and 1.0** with the `random()` method

```py
  random.random()       # 0.645173684807533
```

### Genrate a random integer

Get a random integer **between two specified integers**

```py
  random.randint(1, 100)    # 49
```

### Select a random element

To get a randomly **selected** element **from a non-empty sequence** use the
`choice()` method. **If** an **empty sequence** is provided it will raise an
`IndexError` [error](./t7gf.md)

```py
  random.choice('computer')             # 't'
  random.choice([12,23,45,67,65,43])    # 45
```

### Shuffle elements randomly

To **randomly reorder** the **elements** in a [list](./7cxo.md) use the
`shuffle()` method

```py
  numbers=[12,23,45,67,65,43]
  random.shuffle(numbers)
  print(numbers)                        # [23, 12, 43, 65, 67, 45]
```
