# lang.py.module.openpyxl

Work with excel files

## Synopsis

```py
  from openpyxl import Workbook

  workbook = Workbook()
  sheet = workbook.active

  sheet['A1'] = "Hello World"

  workbook.save(filename="hello_world.xlsx")
```

## Overview

You can use the `openpyxl` mmodule to read from, create and modify `Excel` files

- Provides basic read and write operations on excell files
- A more robust alternative is [xlwings](./1brc.md)
