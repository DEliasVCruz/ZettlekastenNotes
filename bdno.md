# lang.py.module.excel.openpyxl.row_cols

Manipulate and manage rows and columns of a sheet

## Synopsis

```py
  row_1 = sheet[1]
  col_1 = sheet['A']
```

## Overview

You can do most of the operations you can do with rows and columns in an
`excel` file

## Cookbook

### Insert or delete rows

You can insert rows with `insert_rows()` and delete them with `delete_rows()`

- `insert_rows()`: Inserts rows **starting before** the **index number**
- `delete_rows()`: Deletes rows **starting at** the **index number**

Both methods receive the following arguments

- `idx`: The index number to start before or from
- `amount`: The number of rows to create or delete (**default 1**)

```py
  sheet.insert_rows(idx=2)              # Insert a row before row 2
  sheet.delete_rows(idx=2)              # Delete row 2
```

### Insert or delete columns

You can use a similar set of methods to insert and delete columns

- `insert_cols()`: Inserts columns **starting before** the **index number**
- `delete_cols()`: Deletes columns **starting at** the **index number**

They take the **same arguments as** their **rows counterpart**

```py
  sheet.insert_cols(idx=3, amount=2)    # Insert two columns before col 'C'
  sheet.delete_cols(idx=3, amount=2)    # Delete columns 'C' and 'D'
```

### Freeze rows or columns

You can freeze rows or columns so that they **won't move when you scroll through**
your `excel` file for ease of visualization of your data

You have to pass the **row, column or cell** that will serve as the **freeze
pivot** to the `freeze_panes` attribute of your [sheet](./tmox.md) object

```py
  sheet = workbook.active
  sheet.freeze_panes = 'B2'         # Freeze everything before cell 'B2'
  sheet.freeze_panes = 'A2'         # Freeze the first row
```

### Hide rows or columns

You can hide (fold) rows or columns with the `[column|row]_dimensions.group()`
method of the **sheet object**

- The first argument is the row or column to start hiding from
- The second argument is the last row or column to hide
- The third argument is `hidden=True` to hide the row or columns

```py
  sheet.column_dimensions.group('A','D', hidden=True)
  sheet.row_dimensions.group(1,10, hidden=True)
```
