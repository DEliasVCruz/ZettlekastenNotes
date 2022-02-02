# lang.py.module.pandas.accessors.datetime

Operate on Series as datetime objects

## Synopsis

```py
  series.dt.<methods>
```

## Overview

To work with the values of your `Series` object as **datetime** objects you
need to use the `dt` [accessor](./4sli.md)

## Turn a datetime object into a generic time representation

You can turn the elements of a `Series` that represent **datetime** objects
into generic time representations such as

- `day_name()`: Return the index labels as their **corresponding day names**
- `hour`: Return the index labels as their **corresponding hour**
- `year`: Return the index labels as their **corresponding year**
- `quarter`: Return the index labels as their **corresponding quarter**

```py
  dates = pd.Series(pd.date_range('2017', periods=9, freq='Q'))

  dates.dt.day_name()             # Replace dates with their day name ("Monday")
  dates.dt.quarter                # Replace dates with their quarte number (1)
```

## Check a condition of the daytime element

You can check certain datetime related conditions about the elements of your
`Series` and it will return a vectorized `Series` of booleans.

- `is_year_end`: Check if the date correspond to the end of a year

With this you can perform [filtering](./niq3.md)

```py
  daterng[daterng.dt.is_year_end]
```
