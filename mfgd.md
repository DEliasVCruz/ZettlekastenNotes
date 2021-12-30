# lang.py.module.pandas.sorting

How to sort a dataframe based on field values

## Synopsis

```py
  df.sort_values(by=<[field(s)]>[, <extra-arguments>])
```

## Overview

You can perform **sorting** on the entire [dataframe](./5t4z.md) with the `sort_values()`
method. It takes **only one mandatory argument** than **can be** a **single column**
(as a string) **or** a **list of columns**

In **case** a **list** is provided, **sorting** will be performed **in the
order of the elements in the list**

### Arguments

- `by`:
  - **Recieves** a [list](./7cxo.md) or a single [string](./4t3v.md)
  - The fields to sort by
  - Sorting order is based on the order of the elements in the list
- `ascending`:
  - **Recieves** a [boolean](./6auy.md)
  - If `True` it sorts in ascending order (lower to higher)
  - If `False` it sorts in descending order (higher to lower)
- `key`
  - **Recieves** a [function](./8xrz.md) or a [lambda](./8uan.md) expression
  - Sort **baased on** the **results of mapping** the passed **function** to
    each field in the column

## Cookbook

### Sort a dataframe based on more than one column

You can **sort a dataframe according to the values of more than one column** by
passing a list as the `by` argument. The order of the sorting will be based on
the order of the elements in the list

Sorting **does not mutate your original dataframe**, it returns a new sorted
dataframe

```py
  import pandas as pd

  df_exams = pd.read_csv('StudentsPerformance.csv')
  df_exams.sort_values(['math score', 'lang score'], ascending=False)

# Output

# The dataframe sorted first by the 'math score' and
# then by the 'lang score' both in descending order
```

### Sort based on processed value

You can perform **sorting based on a different criteria** by passing a function
that processed the values of the column and return the criteria to sort on with
the `key` argument

```py
  import pandas as pd

  df_exams = pd.read_csv('StudentsPerformance.csv')
  df_exams.sort_values('race', key=lamda col: col.str.lower())
```
