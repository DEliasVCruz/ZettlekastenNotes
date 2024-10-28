# lang.py.module.pandas.index.sorting

Sorting base on the row index or column labels

## Synopsis

```py
  index_sorted_df = df.sort_index()
```

## Overview

Unlike [sort_values](./mfgd.md) this will perform sorting **based on** the
**row index** or [column](./6j2u.md) **names** and **not** by their **values**

When you perform sorting, [filtering](./m2xg.md) or drop [rows](./5t4z.md) the
index label get messed up. You can sort based on this index numbers or labels
with `sort_index()`

> **Rember**: By default the result of `sort_index` returns a copy of the
> original dataframe after being sort, the original dataframe is unafected

## Cookbook

### Sort rows based on index

After applying sorting the original index labels may have become out of order.
You can sort them back with `sort_index()`. By default it applies ascending
sorting

```py
  sorted_df = df.sort_values(by=["make", "model"])
  sorted_df.sort_index(ascending=True)
```

### Sort the columns of your dataframe

You can **sort** your **colummns** with the `axis="columns"` argument, so that they
will be in ascending or descending order **based on** their **label names**.

> You can also use the `columns` name or the number `1`

```py
  df.sort_index(axis="columns", ascending=False)
  df.sort_index(axis=1, ascending=False)    # Same result as before
```
