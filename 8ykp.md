# lang.py.syntax.sorting

Perform sorting of the data contained in diferent types

## Synopsis

```py
  new_data = sorted(data, [reverse=True], [key=<function>])
```

## Overview

You can perform **sorting on different data types** with the `sorted()` built-in
function. This will **not mutate your original data**, but output a new data set

Some data structures you can sort:

- [Lists](./7cxo.md)
- [Tuples](./hsr4.md)
- [Dictionaries](./0loj.md)

## Cookbook

### Sort on descending order

By **default** it will sort the data in **ascending order**, **if** you want to
**sort** it in **descending** order used the `reverse=True` argument

```py
  data = [3, 5, 2, 4, 1]
  sorted_data = sorted(data, reverse=True)      # [5, 4, 3, 2, 1]
```

### Sort base on an arbitrary key

By defualt it will try to sort based on the [ordinal](./4t3v.md) value of the
elements in the data set.

You can **sorted based on the result** that a [function](./8xrz.md) **return
for each** element in the **data set** with the `key=<func>` argument.
This **takes** a **function** and **applys it to each element** of the data
set and the performs sorting based on the returned values

- But keep in mind that it **will not mutate the values** of the data set only
  sort them based on the results

In this example it will apply the `abs()` function on every element and sort
based on their absolute number

```py
  data = [-3, -2, 1, 4]
  sorted_data = sorted(data, key=abs)           # [1, -2, -3, 4]
```

- It also accepsts a [lambda](./8uan.md) function expression

```py
  data = [-3, -2, 1, 4]
  sorted_data = sorted(data, key=lambda x: x % 2)   # [-2, 4, -3, 1]
```

### Sort a class instances based on one of their attributes

**If** the **elements** in your data set are some **class instances**, you can
sort them based on a specific attribute with the `key=<func>` argument

In this case this **lambda** function returns the **element of the class instance**
and then **sorted based** on that element value

```py
  employees = [emp_1, emp_2, emp_3]
  sorted_employess = sorted(employees, key=lambada x: x.name)
```
