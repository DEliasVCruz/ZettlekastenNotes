# lang.py.module.numpy.array

Basic numpy unit for creating multidimensional data

## Synopsis

```py
  import numpy as np

  vector = np.array(<data>)
```

## Overview

The basic unit in `NumPy` is an array and it can have an arbitrary number of
dimension

### Attributes

All **arrays** share this **attributes**:

- `.shape`: **Check the dimensionality** of your array as a [tuple](./hsr4.md)
- `.size`: Check the **total number of values** in your array

## Cookbook

### Create a basic numpy array

When done **manually** they are usually **created from** a [list](./7cxo.md)

```py
  import numpy as np

  vector = np.array([[1, 2, 3], [4, 5, 6]])
  vector.shape

# Out: (2, 3)
"""
  An array of two dimentions
    - Two rows
    - Three columns
"""
```
