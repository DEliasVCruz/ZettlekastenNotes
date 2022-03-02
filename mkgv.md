# lang.py.module.pandas.series

The basic unit of structure of a dataframe

## Synopsis

```py
  from pandas import Series

  s1 = Series(<data>[, <index>])
```

## Overview

Series **represent rows on a** [dataframe](./5t4z.md) and by themselves are **one
column** tabular data where the **values of** it's **index** would be the
**column values** of the **dataframe** they are part of

When performing operations between `Series` data it will **match** the **values
of rows with the same** [index](./271q.md) and perform the operations

It **matches the corresponding keys** to get the values and perform the
operations

- If it can't find matching indexes for a given index, by default, it will not
  perform the operation and fill it with a `NaN` value

- If the indexes are not in matching order it will match them in the best way
  that it can, and **unionize the indexes in order as the resulting series**

- When there are **duplicate index values** in **one or both sides of a
  series**, operations are done as the **cartesian product of all matching
  labels**, and the **result** will be `n` rows with the same label for the
  number of combinatory results

## Cookbook

### Get the index of a `Series`

If you want to get the index of a series as an `Index` ojbect you can use the
`index` attribute you can then operate on it as a normal [index
object](./271q.md)

```py
  s1.index.get_loc(1)
```

### Add up `Series` values

You can add up `Series` object with either the `+` operator or the `add()`
method of a `Series`

```py
  new_s = s1 + s2
  new_s = s1.add(s2, fill_value=0)
```

### Expand nested values in the data of a `Series`

You may have a `Series` that each row has some nested structure. You can **expand**
this **nested values into individual consecutive rows** with the `explode()` method

- This **will repeat the index** for each unpacked value

```py
  ser := pd.Series([[1, 2], [4, 5]])

# 0    [1, 2]
# 1    [4, 5]

  ser.explode()

# 0    1
# 0    2
# 1    4
# 1    5
```

### Set the name of `Series`

In a `Series` object it's **name** it's what would be **used as the row label** when
inserted into a dataframe as a new row
