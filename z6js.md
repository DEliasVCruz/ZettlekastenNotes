# lang.py.module.pandas.index.manipulation

Work with the index structure and data

## Synopsis

```py
  [ser|df].[<index-operation>|index.<operation>]
```

## Overview

You can perform several **manipulation** to the **data and structure** of the
index such as:

- **Index structure**:

  - `.rename_axis()`: **Rename** an index axis and not it's contents
  - `.set_index()`: Set columns of the dataframe as part of the index
  - `.reset_index()`: Move a level of the index into the data as a column
  - `.swaplevel()`: Swap the levels of the index
  - `.reorder_levels()`: Reorder the levels of the index given some order

- **Index data**:

  - `.set_axis()`: Change the values of an index axis based on an array like
  - `.rename()`: Change the values of an index axiss based on a mapper

- **Index creation**:

  - `.difference()`: Create new index object from parts of another index

## Cookbook

### Rename the index axis

You can rename the index axis of your dataframe with the `rename_axis()`
method. If you have a **hierarchical index** then you **can pass a list** for the
**name of every part** of the index

- `axis='columns'`: To make it work with the column axis

```py
  day_names = df.index.day_name()
  hr = df.index.hour

  df.groupby([day_names, hr])["co"].mean().rename_axis(["dow", "hr"])
```

### Set columns as part of the index

You can **indicate** that a column will **serve as the index** of the dataframe with
the `set_index()` method

- By **default** this will **replace any existing index**

```py
   indexed_df = df.set_index('Id')
```

You can also **specify more than one column** as the index of your dataframe
and create a **hierarchical index**

```py
  multi_index_df = df.set_index(['Brand', 'Model'])
```

With the `append=True` argument you can add a column as part of the existing
index instead of replacing it

```py
  df = df.set_index('Id', append=True)
```

### Set an index level as a column of the dataframe

An opposite operation to `set_index()` is the `reset_index()` method that will
**extract** a **level** of the **index** and **insert it** into the data **as a
new column**

- This **level** can be **referenced either by** it's `zero-index` number or
  it's name

```py
  multi_index_df = df.set_index(['Brand', 'Model'])
  single_index_df = multi_index_df.reset_index('Model')

  bool('Model' in single_index_df.columns)                  # True
```

### Remove an index level from your dataframe

You can also use the `reset_index()` method alongside it's `drop=True`,
parameter to remove an index from your dataframe entirely

```py
  multi_index_df = df.set_index(['Brand', 'Model'])
  single_index_df = multi_index_df.reset_index('Model', drop=True)

  bool('Model' in single_index_df.columns)                  # False
```

You can achive the same result using the `droplevel()` method directly

```py
  multi_index_df = df.set_index(['Brand', 'Model'])
  single_index_df = multi_index_df.droplevel('Model')

  bool('Model' in single_index_df.columns)                  # False
```

### Reorder the levels of a hierarchical index

You can reorder the levels of your hierarchical index with either:

- `swaplevels()`: Swap the two index levels
- `reorder_levels()`: Reorder the levels of the index based on some give order

```py
  df = df.set_index(['Brand', 'Model'])
  df.swaplevels()
  df.reorder_levels(['Brand', 'Model'])
```

### Change the values of an index based on array like

You can change the values of an index axis by providing an array like of the
same shape with the `set_axis()` method

```py
  df.set_axis(df.colums.str.title(), axis='columns')
```

### Change the values of an index using a mapper

You can also use the `rename()` method to change the values of an index axis by
mapping a callable to each element in the index

- **Not a vectorized** operation so **probably slower**
- The **default axis** is **rows**
- You can **specify the axis level** with the `level=` parameter
- It also **accepts** a [lambda](./8uan.md) function

```py
  df.rename(str.title, axis='columns')
```

### Select everything but some part of the index data

You can use the `difference()` method to get an **array like** index consisting
of **every element of the original index except some specified values**

The left out values must be **specified inside** an **array like** (ex.
[list](./7cxo.md))

```py
  new_index = df.columns.difference(['Occupation'])
```
