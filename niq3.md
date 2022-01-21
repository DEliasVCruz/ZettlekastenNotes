# lang.py.module.pandas.filtering

You can perform filtering of the dataframe

## Synopsis

```py
  filter_ = <boolean-array>|<boolean-series>
  df[filter_]
```

## Overview

You can perform **filtering** of **the rows** in your [dataframe](./5t4z.md)
with **boolean indexing**.

If you **apply** some **logical operation on** a `series` object, then you’ll
**get another** `series` **with** the **boolean values** `True` and `False`

You can then **_pass_** that `series` **as an index** to your dataframe and it will
**return** a **dataframe where the corresponing row value is** `True`

You can **combine multiple expression** in your filter index with **logic
operators**:

- `~`: The **NOT** logic operator for **negation**
- `&`: The **AND** logic operation for **conjuction**
- `|`: The **OR** logic operation for **at least one true**
- `^`: The **XOR** logic operation for **both true or both false**

This **does not perform mutation** on your original dataframe and instead
returns a new dataframe object

```py
  df[(df['py-score'] >= 80) & (df['js-score'] >= 80)]
```

## Cookbook

### Get only the rows that have mising values

You can filter based on wheter the values of a row are `NaN` with the
`isnull()` method

```py
  df[df['py-score'].isnull()]
```

You can also filter based on rows that don't have missing values with
`notnull()` method

```py
  df[df['py-score'].notnull()]
```

### Remove duplicate values

You can remove duplicate values from your dataframe with the
`drop_duplicates()` method

```py
  no_duplicates_df = df.drop_duplicates()
```

### Filter inside an accessor

You can also use `loc[]` and pass a conditional expression filter for the rows

```py
  nba.loc[nba["fran_id"] == "Lakers", "team_id"].value_counts()
```

### Filter based on string values

You can use the `str` **attribute** on your column to use [string](./4t3v.md)
**methods or operations** on it and perform filtering

```py
  ers = nba[nba["fran_id"].str.endswith("ers")]
```

### Filter based on a regular expresion

You can also use the `cointains()` method on a series/dataframe with the `str`
attribute. With this you can **check if** the **string values match** a **regular
expression**

```py
  df[df["Names"].str.contains("iel")]
```

### Filter based on empty values

You can **check for emptyness** in the values of your column with the `empty`
attribute

```py
  df[~(df["Notes"].empty)]      # Get all non emtpy "Notes" columns
```
