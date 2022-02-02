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

You can also filter based on rows that don't have [missing values](./yptc.md) with
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
  df[~(df["Notes"].empty)]           # Get all non emtpy "Notes" columns
```

### Filter based on datetime objects

You can filter based on the attributes of a datetime object with the `dt`
[datetime accessor](./umhf.md)

```py
  df[df["Date"].dt.quarter > 2]      # Date is over the second quarter of the year
```

### Filter based on index or column labels

You can filter based on the names of the [index labels](./271q.md) or the
[column names](./6j2u.md) rather than on it's contents with:

- `filter()` method:

  - `axis`: Wheter to operate on column names or index labels
    - `0`: **Default**, filter based on **index labels**
    - `1`: Filter based on **column names**
  - `regex`: Use a [regular expression](./cbw4.md) as the filter criteria

```py
  filetered_columns = df.filter(regex=r"^Grade [A-Z]$", axis=1)
```

### Create array of booleans based on index filtering

You can **use** the `isin()` method **to get** a `Series` object of
**booleans** that can be passed as an array like for general filtering

Unlike the `filter()` method that will return a dataframe of filter rows or
columns.

```py
  df.set_index('date_time', inplace=True)
  df[df.index.hour.isin(range(5, 10))]  # Get rows where hour is between 5 and 10
```
