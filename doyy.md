# lang.py.module.numpy.routines

Numpy has a rich api as built-in functions for common tasks

## Synopsis

```py
  import numpy as np
```

## Overview

There are many **functions** that numpy can do from it's **built in api**
called `routines`

- `.clip()`: Create a new array from an existing on by bounding it's values
  - Makes sure the **values don’t exceed a given minimum or maximum**

- `.vecotrize()`: Turn a python function into a vector operation compatible function

## Cookbook

### Turn a regular python function into a vectorized function

If you want **regular** python [functions](./d1jy.md) that where **not design**
with **vector operations** in mind, to **operate in a vectorized manner** you
need to vectorized them with the `vecotrize()` function

There is a few **things to note about** the vectorized function:

- Does not increase function performance
- A thin wrapper for a `for loop` implementation
- Improves readability when using regular python functions in vector operations

```py
  from math import e, factorial

  import numpy as np

  fac = np.vectorize(factorial)

  def e_x(x, terms=10):
      """Approximates e^x using a given number of terms of
      the Maclaurin series
      """
      n = np.arange(terms)
      return np.sum((x ** n) / fac(n))
```
