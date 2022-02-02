# lang.py.module.copy

Create shallow and deep copies of arbitrary Python objects

## Synopsis

```py
  import copy
```

## Overview

When assigning an object to a variable you are not really creating a copy of
the object but a new name for a reference to that object

To actually create an independent copy you have two options

- **Shallow copy**:

  A semi independent of your original object, where the elements of the new
  object are reference to the elements of the previous object

  So affecting the elements on the original object that are referenced in the
  new one, will affect the reference in the new object

  But any other operation that affects non-referenced elements in either object
  will remain independent

```py
  x = [[1, 2], [3, 4]]
  y = list(x)

  x.append([5, 6])
  print(x)                  # [[1, 2], [3, 4], [5, 6]]
  print(y)                  # [[1, 2], [3, 4]]

  x[0][1] = 'x'
  print(x)                  # [[1, 'x'], [3, 4], [5, 6]]
  print(y)                  # [[1, 'x'], [3, 4]]
```

- **Deep copy**:

  This is a completely independent copy of the original object without any
  reference to the elements of the original object

You can **use the copy module** to create **deep and shallow** copies of
**arbitrary** `Python` **objects**

## Cookbook

### Create a shallow copy of an object

You can create a **shallow copy** with the `copy()` function

```py
  import copy

  x = [[1, 2], [3, 4]]
  y = copy.copy(x)
```

### Create shallow copy for built-in types

Most built-in type objects have a `copy()` method to create a shallow copy of
the instance

- `[].copy()`: Create a shallow copy of a [list](./7cxo.md)
- `{}.copy()`: Create a shallow copy of a [dictionary](./0loj.md)

```py
  list_1 = [1, 2, 3]
  list_2 = list_1.copy()

  print(list_1 is list_2)       # False
```

### Create a deep copy of an object

You can create a **deep copy** with the `deepcopy()` function

```py
  import copy

  x = [[1, 2], [3, 4]]
  y = copy.deepcopy(x)
```
