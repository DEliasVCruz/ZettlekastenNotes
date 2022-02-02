# lang.py.module.pandas.replace

Replace data in your columns in a vectorized way

## Synopsis

```py
  mapping = {<value-1>: <replacement-1>, <value-2>: <replacement-2>}
  df_replaced = df.map(mapping)
```

## Overview

There are many ways to replace data in your dataframe, but one way to do it for
many **replace values** is **with** the `map()` method

This takes a [dictionary](./0loj.md) where the **keys represent** the **values
in** your `Series` to replace and the **dictionary values** are the **replacing
values**

## Cookbook

### Replace many values with a specified replacement

If you wanted to replace one substring with another for all elements in your
`Series` you could use the `str` [string accessor](./m0jc.md) with the `replace()`
method

But if you wanted to **replace many substring** with **specified replacement
values** then it's better to use `map()`

**In this example** any substring with that matches the keys in the dictionary
will be replaced with it's value

```py
  mapping = {'first': 1, 'second': 2, 'third': 3}

  df_replaced = df.map(mappingj)
```

### Reaplace based on ranges of data (`pd.cut()`)

If you want to do replacement where the **replaced data** is a **series of
ranges** that will be **mapped to one value**, then your best option is to use
[cut](./rpm8.md)

- `bins`: A [list](./7cxo.md) of ranges to do the replacement on
- `labels`: The value that will replace their corresponding range

```py

```
