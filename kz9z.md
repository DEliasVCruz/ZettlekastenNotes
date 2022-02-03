# lang.py.module.excel.openpyxl.workbook

Create or load an excel file

## Synopsis

```py
  from openpyxl import Workbook, load_workbook

  workbook_1 = Workbook()
  workbook_2 = load_workbook(filename='excel_file.xlsx')
```

## Overview

The basic `excel` file can be created or loaded from an existing `excel` file with

- `Workbook()`: Create an `excel` file object
- `load_workbook()`: Create an `excel` file object from an existing file

## Cookbook

### Create a workbook object

You can create a new `excel` file and operate on it as a workbook with the
`Wokrbook()` class

- You can then **save it as a new file** with the `save()` method

```py
  from openpyxl import Workbook

  workbook = Workbook()
  workbook.save('my_file.xlsx')
```

### Load an existing excel file

To **use an existing file** as your workbook to operate on use the
`load_workbook()` function

- `filename`: The name of the file path
- `read_only`: Load the file as read only (**good for very large files**)
- `data_only`: Ignores loading formulas and only loads resulting values

```py
  from openssl import load_workbook

  woorkbook = load_workbook(filename='my_file.xlsx',
                            read_only=True, data_only=True)
```
