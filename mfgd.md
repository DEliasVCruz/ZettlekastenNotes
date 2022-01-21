# lang.py.module.pandas.sorting.values

How to sort a dataframe based on column or row values

## Synopsis

```py
  df.sort_values(by=<[field(s)]>[, <extra-arguments>])
```

## Overview

You can perform **sorting** on the entire [dataframe](./5t4z.md) with the `sort_values()`
method. It takes **only one mandatory argument** than **can be** a **single column**
(as a string) **or** a **list of columns**

Unlike [sort_index](./bzog.md) this will perform sorting **based on** the
**values** of a column or row

In **case** a **list** is provided, **sorting** will be performed **in the
order of the elements in the list**

### Arguments

- `by`:
  - **Receives** a [list](./7cxo.md) or a single [string](./4t3v.md)
  - The fields to sort by
  - Sorting order is based on the order of the elements in the list
- `ascending`:
  - **Receives** a [boolean](./6auy.md) **or** a **list of booleans**
  - If `True` it sorts in ascending order (lower to higher)
  - If `False` it sorts in descending order (higher to lower)
- `key`
  - **Receives** a [function](./8xrz.md) or a [lambda](./8uan.md) expression
  - Sort **based on** the **results of mapping** the passed **function** to
    each field in the column
- `axis`: **Indicate** to sort by rows (`axis=0`) or columns (`axis=1`)
- `na_position`: Whether you want rows with `NaN` to appear first
- `kind`: The type of **sorting algorithm** to use
  - This is **ignored when** sorting on **more than one column**
  - `quicksort`: Default sorting algorithm
  - `mergesort`: Stable sorting algorithm
  - `heapsort`: Heap style sorting algorithm

## Cookbook

### Sort a dataframe based on the values of a column

The simple way to sort a dataframe is by passing the name of the column to
`sort_values()` this will by default sort the column in ascending order
according to the values of that column

Sorting **does not mutate your original dataframe**, it returns a new sorted
dataframe

```py
  sortded_df = df.sort_values("Scores")
```

### Sort a dataframe based on more than one column

You can **sort a dataframe according to the values of more than one column** by
passing a list as the `by` argument. The order of the sorting will be based on
the order of the elements in the list

```py
  import pandas as pd

  df_exams = pd.read_csv('StudentsPerformance.csv')
  df_exams.sort_values(by=['math score', 'lang score'], ascending=[False, True])

# Output

# The dataframe sorted first by the 'math score' ind descendig order
# and then by the 'lang score' in ascending order
```

### Sort based on processed value

You can perform **sorting based on a different criteria** by passing a function
that processed the values of the column and return the criteria to sort on with
the `key` argument

```py
  import pandas as pd

  df_exams = pd.read_csv('StudentsPerformance.csv')
  df_exams.sort_values(by='race', ascending=True, key=lamda col: col.str.lower())
```

### Change the sorting algorithm

You can change the sorting algorithm with the `kind` argument. It can take any
of three merge algorithm

- `quicksort`: Default sorting algorithm
- `mergesort`: Stable sorting algorithm
  - It will maintain the original order of the records with the same key
  - Necessary if you plan to perform multiple sorts
- `heapsort`: Heap style sorting algorithm

This will be ignored if you are sorting on more than one column or label

```py
  df.sort_values(
      by="cityId",
      ascending=False,
      kind="mergesort"
  )
```

### Sort based on missing values

By default, when performing sorting, regardless of the sorting order, missing
values will go at the end of the dataframe.

You can use the `na_position='first'` to put them at the begining of your dataframe

```py
  df.sort_values(by='Notas', na_position='first')
```
