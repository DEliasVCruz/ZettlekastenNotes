# lang.py.module.pandas.write

Write and export your dataframe to many diferent formats

## Synopsis

```py
  df.to_<format>()
```

## Overview

You can **export** your dataframe to different formats:

- json
- csv
- excell

**And more** by extructuring like `<dataframe-object>.to_<format>()`

## Cookbook

### Export a dataframe to other format

You can **export** your dataframe **to different formats**. Some of the
supported formats are:

- `to_excell`: Export your dataframe as an `excell` spreadsheet
- `to_csv`: Export your dataframe as a `csv` file
- `to_numpy`: Export your dataframe as a `numpy` array without the labels

```py
  df.to_excel('excel_table.xlsx', sheet_name="TABLE")
  df.to_csv('excel_table.csv')
```

### Extract data as a numpy array

Sometimes you may want to **extract data** from your dataframe **as a list without
it's labels**, just the data. For that you can use the `to_numpy()` method, that
will return a [numpy](./5nfr.md) **array of just the data without the column
names or index names**

The `to_numpy()` is the same as `values()` with the **added functionality** of
specifying the **optional arguments**:

- `dtype`: Set to [None](./y624.md) by default. Serves to **specify the type of
  the resulting array**
- `copy`: A [boolean](./6auy.md) for which
  - `False`: The data is tied to the dataframe and changes accordingly
  - `True`: Make a new copy detach from the original dataframe

```py
  df.to_numpy()
```
