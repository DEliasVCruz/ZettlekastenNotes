# lang.py.module.csv.write

Write csv files

## Synopsis

```py
  import csv
```

## Overview

You can write your data into a csv file either manually or from a dictionary
with the `writer()` and `DictWriter()` objects respectively

## Cookbook

### Write data into a csv file

You can use the `writer()` object to write into a csv file, alongside the
`.writerow()` method of the **writer object**.

You can **specify** the **delimiter character** and whether to **use escape
characters** for values that contain the delimiter character

```py
  import csv

  with open('file.csv', mode='w') as csv_file:
      csv_writer = csv.writer(csv_file, delimeter=',')

      csv_writer.writerow(['Name', 'Last Name', 'Age'])
      csv_writer.writerow(['Daniel', 'Vilela', '23'])
```

### Escape delimiter characters

You can use the `escapechar=` and `quoting=csv.QUOTE_NONE` argument to specify
an escape character for elements that include the delimiter character

```py
  with open('file.csv', mode='w') as csv_file:
      csv_writer = csv.writer(csv_file, delimeter=',',
                              escapechar='\', quoting=csv.QUOTE_NONE)

      csv_writer.writerow(['Mario', 'Vor,Band', '25'])

```

### Write a dictionary into a csv

You can **write** a [dictionary](./0loj.md) **for each row** in your csv file
with the `DictWriter()` object

You have to **specify** the **field names** with the `fieldnames=` as a
[list](./7cxo.md) and then using the `writeheader()` method on your writer
object

```py
  with open('file.csv', mode='w') as csv_file:
      fields = ['Name', 'Last Name', 'Age']
      csv_writer = csv.DictWriter(csv_file, fieldnames=fields)

      csv_writer.writeheader()
      csv_writer.writerow({'Name': 'Daniel', 'Last Name': 'Vilela', 'Age': 23})
      csv_writer.writerow({'Name': 'Jose', 'Last Name': 'Octavio', 'Age': 19})
```
