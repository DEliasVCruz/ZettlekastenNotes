# lang.py.module.pandas.index.stacking

Turn row indices into columns and vise versa

## Synopsis

```py
  df.unstack()
  df.stack()
```

## Overview

You can use the `unstack()` and `stack()` methods to turn a rows
[index](./271q.md) into a columns index and columns index into rows index
respectively

They support some of the following **arguments**:

- `fillvalue`: What to use for **missing values**
- `level`: The index level to stack or unstack (**can be index name**)

## Cookbook

### Make a row index into a column index

If you have a `hierarchical index` you can turn one of the row index into a
column index with the `unstack()` method

By **default** it will **unstack** the **last level** of the `zero-based` index

```py
  df.groupby(['Station', 'Year'])['Sales'].sum().unstack(level=1, fill_value=np.nan)
```

### Make a column index into a row index

You can turn your [column](./6j2u.md) index into part of your row index with
the `stack()` method

```py
  df = df.groupby(['Station', 'Year'])['Sales'].sum().unstack(level="Year")
  df.stack()
```
