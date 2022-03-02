# lang.py.module.pandas.transform

Operate on your grouped series and preserve indexing

## Synopsis

```py
  [ser|df].groupby(<grouping>).transform(<>)
```

## Overview

You can use `transform` to do some **non reducing/aggregation** operation on the
group elements of your series

- This will effectively **keep the original** [indexing](./271q.md) of your data
- Works on a [Series](./mkgv.md) basis

## Cookbook

### Perform some operation on all the elements of groups

If you need to **perform some non reducing operation** on all the elements of
groups of your data and **preserve the original index** of your dataset

- This is **best when** doing some sort of **data normalization**

```py
  from numpy import zscore

  ser.groupby(s.index.to_period('M')).transform(zscore)
```
