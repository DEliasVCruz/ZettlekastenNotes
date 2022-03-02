# lang.py.module.numpy

Core library for multidimensional vectorized operations

## Synopsis

```py
  import numpy as np
```

## Overview

There are three main concepts you need to **use numpy effectively**:

1. Creating [arrays](./5nfr.md) using `numpy.array()`
2. Treating complete arrays like individual values to make vectorized
   calculations more readable
3. Using built-in `NumPy` functions to modify and aggregate the data

### Basics

- **Vectorization**:

  **Performing the same operation** in the same way **for each element** in an
  array, this removes for loops

- [Broadcasting](./92ab.md): Match arrays dimensions so they can be operated against

- **Scalar**: A vector of a single value (**shape (1,)**)
- **Vectors**: One dimensional arrays
- [Mask](./3f8p.md): An array with the same shape of your original array but
  with [boolean](./6auy.md) values
