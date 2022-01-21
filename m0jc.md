# lang.py.module.pandas.strings

Working with string values in your datarame

## Synopsis

```py
  df[<column>].str.<methods>()
```

## Overview

You can operate on the values of your [dataframe](./5t4z.md) like strings and
have **access** to **regular string methods** as well as other **extra ones**

- `contains()`: Returns a series objects with [booleans](./6auy.md)
- `replace()`: Replace the matching regex with other string
- `extract()`: Replaces values with matching regex expression
  - Replaces with `NaN` [missing values](./yptc.md) if not matched

## Cookbook

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

### Extract values based on a regular expression

You can use the `extract()` method from the dataframe str attribute to [replace
the values](./67tx.md) with the matched [regular expression](./cbw4.md) or
`NaN` in case the regex is not matched

```py
  extr = df['Date of Publication'].str.extract(r'^(\d{4})', expand=False)
  df['Date of Publication'] = extr
```

### Replace values based on a regular expression

YOu can replace a matched regex with another substring with the `replace()`
method and **leave the rest intact**

```py
  df['Place of Publication'] = df['Place of Publication'].str.replace('-', numpy.nan)
```
