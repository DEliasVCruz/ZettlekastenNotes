# lang.py.module.dates.datetime

Built-in module to handle dates and datetime data

## Synopsis

```py
  from datetime import datetime
```

## Overview

## Cookbook

### Create a date from a string representation

You can use the `strptime()` function to create a date object from
the [string](./4t3v.md) representation of the date

- You need to specify the format of the given string date
- You use date formatter expresion
  - `%Y`: Year with the full number (1998)
  - `%y`: Year in the abrevation format (98)

```py
  from datetime import datetime

  date = datetime.strptime("2013-1-25", "%Y-%m-%d")
```

### Change the format of a date

You can change the format of date object with the `strftime()` and it
returns a string representation of the formated date

- The **result is not a datetime object**

```py
  import datetime

  now = datetime.strptime("1998-07-04", "%Y-%m-%d")
  normal_date_str = now.strftime("%d/%m/%y")
  print(normal_date_str)                        # 04/07/98
```
