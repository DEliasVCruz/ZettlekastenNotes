# lang.py.module.pandas.mising_data

Missing data representation and handling with pandas

## Overview

Missing data in a [dataframe](./5t4z.md) is represented as `NaN` (**not a number**)

You can get `NaN` with:

- `float('nan')`
- `math.nan`
- `numpy.nan`

When [operations](./l1ya.md) or calculations are **perform** on rows or columns
with `NaN` values **most method ommit them** and perform the calculation
without taking the missing values into account

### Filling missing data

You can replace missing data (`NaN`) with other values with the `fillna()`
method:

- `value`: Replace **every** `NaN` **with** the especified **value**
- `method`: Replace with either the value before or after
  - `ffill`: **Replace with** the **value before** the `NaN` value
  - `bfill`: **Replace with** the **value after** the `NaN` value

```py
  df.fillna(value=0, inplace=True)   # Replace NaN values with 0

  df["Notes"].fillna(                # Replace missing values of specific column
    values="no notes",
    inplace=True
  )

  df = df.fillna(method='ffill')     # Replace NaN values with the value before it
```

You **can also apply interpolation to fill the missing value** with the ponderation
of the previous and next value

```py
  df = df.interpolate()              # Replace NaN values with interpolation
```

This methods **do not perform mutation** on the original dataframe, instead they
return a new `series` or dataframe object

### Drop null values from a dataframe

When **performing clean up** on your dataframe, you may want to **remove any row
that has null values**. For that we use the `dropna()` method

It **returns a new dataframe**, if you want to **mutate** your **original**
dataframe **use** the `inplace=True` argument or re assign it to the original
dataframe

```py
  df_population = df_population_raw.dropna()
```

### Drop columns with missing values

To drop all columns that have missing values you can **pass** the `axis=1` argument
to the `dropna()` method

```py
  data_without_missing_columns = df.dropna(axis=1)
```

### Check for null values

You can [filter](./m2xg.md) your rows based on wether they have or not `NaN`
values with `isnull()` and `notnull()` methods

```py
  df[df['py-score'].isnull()]
  df[df['py-score'].notnull()]
```

### Check for emptyness in your dataframe

You can **check** if a [filter](./niq3.md) **returns** an **empty** dataframe
with the `empty` attribute

```py
  df[<conditional-filter>].empty        # Returns boolean
```

### Calculate how many rows have mising data

You can **get** the **number of rows** that have `NaN` values with this one liner

```py
  print(df.isnull().values.sum())       # 248
```
