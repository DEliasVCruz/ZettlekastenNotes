# lang.py.module.excel.openpyxl.iterate

How to iterate over the rows and columns of an excel file

## Synopsis

```py
  for [col|row] in sheet.iter_[cols|rows](min_[col|row]=<int>,
                                          max_[col|row]=<int>,
                                          min_[col|row]=<int>,
                                          max_[col|row]=<int>):
    print([col|row])
```

## Overview

You can iterate over a range of rows or columns in with:

- `iter_cols`: Iterate over the specified columns
- `iter_rows`: Iterate over the specified rows

You can specify the range of the rows or columns to iterate over with. You
specify them by their `1 index` label number

- `min_row`: The `1 index` row to start iterating on
- `max_row`: The `1 index` row to stop iterating at
- `min_col`: The `1 index` col to start iterating on
- `max_col`: The `1 index` col to stop iterating at

They return a [tuple](./hsr4.md) with the cells objects for every row or column

## Cookbook

### Iterate over all the rows or columns

You can iterate over all the rows or columns of your [sheet](./tmox.md) or
range object with `rows` and `columns` attributes

```py
  for row in sheet.rows():
      print(row.value)

  for col in sheet.columns():
      print(col.value)
```

### Iterate over the rows of a range of cells

You can specify a **range** of rows and columns **to start and stop iterating**
over **it's rows** with `iter_rows`

```py
  for row in sheet.iter_row(min_row=1,
                            max_row=2,
                            min_col=1,
                            max_col=3):
      print(row)

```

### Iterate over the columns of a range of cells

You can specify a **range** of rows and columns **to start and stop iterating**
over **it's columns** with `iter_cols`

```py
  for col in sheet.iter_cols(min_row=2, max_row=3, min_col=1):
      print(col)
```

### Only get the values of your iteration

You can pass the `only_values=True` parameter to both `iter_rows` and
`iter_cols` to get only the values of the cells in the row or column

```py
  for row_values in sheet.iter_rows(min_row=1, min_col=2, max_col=4,
                                    values_only=True):
      for value in row_values:
          print(value)
```

### Iterate directly on a range object

You can also do a normal `for loop` iteration on your range object

```py
  for cell in sheet[1]:
      print(cell.value)
```
