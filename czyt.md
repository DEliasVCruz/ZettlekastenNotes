# lang.py.module.pandas

Work with structured data like tables

## Synopsis

```py
  import pandas as pd
```

## Overview

The pandas module allows us to work with structured data like tables with a
special type called a data grame

## Cookbook

### Create a dataframe

You can create [dataframe](./5t4z.md) form many types of data types

- Numpy array:
  - Each list in the array will represent a row
  - `data = np.array([[1,4], [2,5], [3,6]])`
- List Array:
  - Each element list in the list will represent a row
  - And each inner element represents a column value
  - `data = [[1,4], [2,5], [3,6]]`
- Dictionaries:
  - Each dictionary key will represent a column name
  - And the values of the key will be the value per row
  - `my_dict = {'column-name': [values]}`
- CSV files:
  - You can read from a csv file
  - `data = pd.read_csv(<csv_file.csv>)`

### Display all columns and their data types

You can display a list of all the columns in your dataframe and the type of
data thy hold

```py
  dataframe.info()
```
