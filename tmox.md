# lang.py.module.openpyxl.sheet

Operate on a workbook standalone sheet object

## Synopsis

```py
  sheet = workbook.active
  print(sheet)
```

## Overview

The **standard object** you are going to be **working with** is the `sheet`
object. It is a colection of `1 index` rows and `alphabetic columns`

## Cookbook

### Get the name of the selected sheet

You can **get** the name of the **currectly selected sheet** with the `title`
attribute

```py
  sheet = worbook.active
  print(sheet.title)        # 'Hoja 1'
```

### List the available sheets in your file

You can get a [list](./7cxo.md) of the available [sheet](./tmox.md) names with
the `sheetnames` attribute

```py
  sheets = workbook.sheetnames
  print(sheets[0])                  # 'Hoja 1'
```

### Select and use the active sheet

You can operate on the **currently active sheet** with the `active` attribute

```py
  active_sheet = workbook.active
```

### Select and use a sheet by it's name

You can access and use a sheet object by **refering to it by** it's name like a
[dictonary](./0loj.md) key in your [workbook](./kz9z.md) object

```py
  sheet = workbook['Hoja 2']
  print(sheet.title)            # 'Hoja 2'
```

### Create a new sheet in your wokbook

You can create new sheets with the `create_sheet()` method

- `index`: Indicate the `0 index` position of the sheet in the list of sheets

```py
  print(workbook.sheetnames)        # ['Hoja 1', 'Hoja 2']

  workbook.create_sheet(title='Nueva', index=1)
  print(workbook.sheetnames)        # ['Hoja 1', 'Nueva', 'Hoja 2']
```

### Delete a sheet from your workbook

You can delte sheets by **passing the sheet object** to the `remove()` method
of your `Workbook` **object**

```py
  print(workbook.sheetnames)        # ['Hoja 1', 'Borrame', 'Hoja 2']

  sheet_to_remove = workbook['Borrame']
  workbook.remove(sheet_to_remove)

  print(workbook.sheetnames)        # ['Hoja 1','Hoja 2']
```

### Copy and duplicate a sheet

You can duplicate a sheet by **passing it to** the `copy_worksheet()` method.

- It will always append them to the list of sheets

```py
  print(workbook.sheetnames)        # ['Hoja 1', 'Copiame', 'Hoja 2']

  sheet_to_copy = workbook['Copiame']
  workbook.copy_worksheet(sheet_to_copy)

  print(workbook.sheetnames)        # ['Hoja 1', 'Copiame', 'Hoja 2', 'Copiame']
```
