# lang.py.module.pandas.apply

Apply a function to every Series of either axis

## Synopsis

```py
  df.apply(<fuction>, axis=[0|1])
```

## Overview

You can use `apply` to [iterate](./zsxw.md) over every `Series` of either the
[rows](./myvh.md) or [columns](./6j2u.md) of a dataframe

The main difference with [applymap](./rtyt.md) method is:

- `applymap)`: Will apply the function to every element in the dataframe
  - It's the **slowest**
  - Operates on every single element of the `dataframe`

- `apply`: Will apply the function to every `Series` object in either the
  columns or rows
  - Is generally **faster**
  - It iterates over the rows or columns and operates on their elements
  - Is **preferable over the standard** row or column iteration of `for loop`
  - It's **better than** `iterrows()`

## Cookbook

### Iterate over every row and operate on them

You can **iterate over every row** of the dataframe and **operate on** it's
**elements** with `axys=1`

The **function must**:

- Take `Series` object as it's argument
- Return a single new element at a time

In the end the `apply` method **will return a new** `Series` object

```py
  def apply_tariff(kwh, hour):
      """Calculates cost of electricity for given hour."""
      if 0 <= hour < 7:
          rate = 12
      elif 7 <= hour < 17:
          rate = 20
      return rate * kwh

  df['cost_cents'] = df.apply(
      lambda row: apply_tariff(
          kwh=row['energy_kwh'],
          hour=row['date_time'].hour),
      axis=1)
```
