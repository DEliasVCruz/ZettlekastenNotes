# lang.py.module.numpy.sorting

Sorting capabilities of the numpy library

## Synopsis

```py
  np.sort(<array>[, <axis>])
```

## Overview

You can use the `.sort()` function to sort the elements of an array, it **takes
an array** and returns a new one

- It will sort the elements of the specified [axis](./bd42.md) dimension

## Cookbook

### Perform a basic sorting of an array

You need to pass the array that is going to be sorted, and **by default** it will
**sort based on** the **last** an innermost **dimension**

```py
  data = np.array([
      [7, 1, 4],
      [8, 6, 5],
      [1, 2, 3]
  ])

  np.sort(data)         # axis = 1

# Out:
  array([[1, 4, 7],
         [5, 6, 8],
         [1, 2, 3]])
```

### Sort on a specified dimension of the array

You can also **specify** what **dimension** is the one **that will get sorted**
with the `axis=<axis-index>` parameter

- And then **all** the **elements of that dimension** will be the ones **sorted**

```py
  np.sort(data, axis=0)

# Out:
  array([[1, 1, 3],
         [7, 2, 4],
         [8, 6, 5]])
```

### Sort all the elements of an array

You can pass `axis=None` and this will **flatten the array** and perform a
**global sort** of all the elements in the array

```py
  np.sort(data, axis=None)

# Out:
  array([1, 1, 2, 3, 4, 5, 6, 7, 8])
```
