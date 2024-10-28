# lang.py.module.pandas.accessors.datetime

Operate on Series as datetime objects

## Synopsis

```py
  series.dt.<methods>
```

## Overview

To work with the values of your `Series` object as **datetime** objects you
need to use the `dt` [accessor](./4sli.md). This will give you some special
**time series** operations

This operations also work directly on a `datetime` [index](./271q.md) objects
without the need of the `dt` accessor

This can be much better than doing direct row or column level
operations since it can take advantage of [vectorization](./1c2p.md) 

## Turn a datetime object into a generic time representation

You can turn the elements of a `Series` that represent **datetime** objects
into generic time representations such as

- `day_name()`: Return the series date values as their **corresponding day names**
- `month_name()`: Return the series date values as their **corresponding month names**
- `hour`: Return the series date values as their **corresponding hour number**
- `year`: Return the series date values as their **corresponding year number**
- `month`: Return the series date values as their **corresponding month number**
- `quarter`: Return the series date values as their **corresponding quarter**

```py
  dates = pd.Series(pd.date_range('2017', periods=9, freq='Q'))

  dates.dt.day_name()             # Replace dates with their day name ("Monday")
  dates.dt.quarter                # Replace dates with their quarte number (1)

  dates.dt.month
# Result
# 0     3
# 1     6
# ...
```

### Turn dates into an specific period representation

If you **don't just want the name or number** of the specific `datetime` component
and you want to **change the period representation** of you date:

- `to_period()`: Change the date to an specific [time series](./6e6x.md) **date frequency**

```py
  dates.dt.to_period('M')

# Result
# 0     2017-03
# 1     2017-06
# ...
```

## Check a condition of the daytime element

You can check certain datetime related conditions about the elements of your
`Series` and it will return a vectorized `Series` of booleans.

- `is_year_end`: Check if the date correspond to the end of a year

With this you can perform [filtering](./niq3.md)

```py
  daterng[daterng.dt.is_year_end]
```
