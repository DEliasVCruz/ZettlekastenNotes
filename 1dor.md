# lang.py.module.excel.openpyxl.format.style

Format the style of the cells and their values

## Synopsis

```py
  from openpyxl.styles import Font, PatterFill, Alignment, Border, Side

  cell = sheet['A1']
  cell.font = Font()
  cell.border = Border(Side())
  cell.aligment = Alignment()
  cell.fill = PatterFill()
```

## Overview

You can modifile the diferent styles of the [cells](./n3z1.md) and values of your
spreadsheet

**Each cell object** has the following **attributes** that can be **modify
by** a similar named class

- `.font`: Change the font style of the value

  - Accepts an instance of the `Font()` class

- `.border`: Change the border style of the selected cell

  - Accepts an instance of the `Border()` class
  - Each border of the `Border` class takes an instance of the `Side` class
  - This applies to the overal cell

- `.fill`: Change the color filling of the selected cell

- `.alignment`: Change the horizontal and vertical aligment of the value

  - Accepts an instance of the `alignment()` class

You can also create an style template with the `NamedStyle()` class that takes
the same attributes as a regular cell and can be reaplied to the `style`
attribute of a cell object

## Cookbook

### Change the font of a cell

You can format the font of the values of a cell with the `Font()` class and
pass it's instance the `.font` attribute of a cell

It accepts some of the following **options**:

- `bold`: Display the font in bold (**boolean**)
- `color`: The color of the font in `hex` code (**string**)
- `size`: The size of the font (**integer**)

```py
  from openpyxl.styles import Font

  red_bold_font = Font(bold=True, color="C70E0F", size=11)
  sheet['A1'].font = red_bold_font
```

### Change the aligment of text in a cell

You can modifiy the aligment of the text value inside a cell by passing the
`Alignment()` class to the `alignment` attribute of the cell

You can chage `horizontal` and `vertical` aligment that **take the values**:

- `center`
- `left`
- `right`

```py
  from openpyxl.styles import Alignment

  horizontal_center_text = Alignment(horizontal='center')
  sheet['A1'].alignment = horizontal_center_text
```

### Change the border style of a cell

You can change the sytle of the borders of a cell by passing the `Border()`
class to the `border` attribute

The `Border()` class takes an instance of the `Side()` class for every side of
the border as a parameter

- `top`
- `right`
- `bottom`
- `left`

With the `Side()` class you can define the individual style of each side of the
border

- `border_style`: Defines the general style of the border side
  - `double`: Double lines as the border
  - `thin`: A thin line as the border

```py
  from openpyxl.styles import Border, Side

  double_style_border = Side(border_style='duble')

  square_border = Border(top=double_style_border,
                         right=double_style_border,
                         bottom=double_style_border,
                         left=double_style_border)

  sheet['A1'].border = square_border

```

### Change the color filling of a cell

You can change the color filling of a cell by passing an instance of the
`PatterFill()` class to the `.fill` attribute of a cell

It accepts some of the **following options**:

- `fgColor`: The **hex color** of the foreground of the cell

```py
  red_background = PatterFill(fgColor='C70E0F')
  sheet['A1'].fill = red_background
```

### Create a custom named style template

You can create a template that can be **directly passed to** the `style`
attribute of a cell and **avoid** having to **access each individual
attribute** for each cell

You have to create a `NamedStyle()` object wich will **have** the **same
formatting attributes** as a **regular cell**

```py
  from openpyxl.styles import NamedStyle, Border, Side, Font, Alignment

  header = NamedStyle(name="header")

  header.font = Font(bold=True)
  header.border = Border(bottom=Side(border_style="thin"))
  header.alignment = Alignment(horizontal="center", vertical="center")

  header_row = sheet[1]

  for cell in header_row:
      cell.style = header
```

### Register a named style

You can register a named style to be part of the file by either:

- Using the `add_named_style()` [workbook](./kz9z.md) method
- Assigning the name style object to a cell for the first time

After that you can **reference the named style** by it's name **as a** [string](./4t3v.md)

```py
  workbook.add_named_style(header)
  sheet['A1'].style = 'header'
```

### Format merged cells

To format a range of merged cell you need to **apply formataing to the top-left
cell of the merged group**

```py
  ws.merge_cells('B2:F4')
  top_left_cell = ws['B2']

  top_left_cell.fill = PatternFill("solid", fgColor="DDDDDD")
```
