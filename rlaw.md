# lang.py.module.csv.read

Read from csv files

## Synopsis

```py
  import csv

  with open('<csv-file>', mode='r') as csv_file:
      csv_reader = csv.reader(csv_file, delimeter=<separator>)
      for row in csv_reader:
          ...
```

## Overview

When reading a csv file it's open as a text file with the `open()` function and
then the file object is [passed](./7i8g.md) to the `.reader()` object

It accepts some of the **following arguments**:

- `delimiter=<string>`: The **separator** for each **column** of the file
- `fieldnames=<list>`: Specify the column names ordered in a [list](./7cxo.md)

## Cookbook

### Read a csv file and specify a delimeter

You can read a csv file by passing it as a file object to the `reader` class
and **specify a delimeter**

**Each line** in the file is represented as a **list** where it's **elements**
are each **column element** for that row **as a** [string](./4t3v.md)

```py
  import csv

  with open('my_csv.csv', mode='r') as csv_file:
      csv_reader = csv.reader(csv_file, delimeter=',')
      headings = next(csv_reader)
      first_column_name = headings[0]

  print(headings)                               # ['Name', 'Last Name', 'Age']
  print(first_column_name)                      # 'Name'
```

### Read a csv into a dictionary

You can read a csv file directly into a dictionary with the `DictReader()`
class.

This will turn **each row** of the csv, after the heading, **as a dictionary**
where the **keys** are the **column names** and the **values** are that **row
corresponding values**

```py
  with open('file.csv', mode='r') as csv_file:
      csv_reader = csv.DictReader(csv_file)
      headings = next(csv_reader)

      first_row = next(csv_reader)
      first_column_value = first_row['Name']

  print(headings)                               # ['Name', 'Last Name', 'Age']
  print(first_column_value)                     # 'Jose'
```
