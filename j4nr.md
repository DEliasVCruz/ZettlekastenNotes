# lang.py.module.pandas.grouping.apply

Perform any operation on your grouped data and get new indexing

## Synopsis

```py
  [ser|df].groupby(<grouping>).apply(<operation>)
```

## Overview

You can use `apply` to **perform any operation** on your grouped data, **be it
aggregating or not**, and that can result in any new index

- You can use this to get a brand new indexing
- This can be a slow operation, if possible avoid it
- It works on a [Dataframe](./5t4z.md) basis

## Cookbook

### Perform a custom aggregation after filtering the group

You **use** this **mostly when** you **want to perform** some **additional**
[filtering](./niq3.md) on your grouped data before doing any operation

```py
  df.groupby("outlet", sort=False)["title"].apply(
      lambda ser: ser.str.contains("Fed").sum()
  ).nlargest(10)
```
