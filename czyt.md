# lang.py.module.pandas

Work with structured data like tables

## Synopsis

```py
  import pandas as pd
```

## Overview

The pandas module allows us to work with structured data like tables with a
special type called a `dataframe`

There are two types of objects defined:

- **Series**: A **single dimension array** (a single column)
- **Dataframe**: A **two dimensional array** (multiple columns)

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

### Create a Series

**Each row** in a `dataframe` is an instance of a `Series` object. To create a new
`Series` object use the `Series()` class

```py
  row = {
      'Column_1'; 'value_colum_1'
      'Column_2'; 'value_colum_2'
      'Column_3'; 'value_colum_3'
    }
  new_sr = pd.Series(row)
```

### Display all columns, amount of not-nulls and their data types

You can display a list of all the columns in your dataframe and the type of
data thy hold. This will **also show** you **the amount of not-null** records in
each column

```py
  df.info()
```

### Display general statistic summary

If you want a **small summary** with some **basic statistic analysis** of your
**dataframe** you can use the `describe()` method

This **will show** you:

- **Count**: How many rows each column has
- **Mean**: The average of the values in the field
- **Standard Deviation**: The difference from the mean
- **Min**: The minimum value in the field
- **Max**: The maximum value in the field
- **Percentiles**: The 25%, 50% and 75% percentiles from the mean

```py
  df.describe()
```

By **default**, `describe` will only perform statistic **analysis** on fields
of **numeric value**. With the `include=object` argument it will also display
statistic analysis **for non numeric values**

This will **also show**:

- **Unique**: How many unique values there are
- **Top**: The most repeated value

```py
  df["Notes"].describe(include=object)      # Describe the "Notes" column
```

### Select a single element of your field

Every column of a dataframe is an instance of a pandas `series` object. So you
can get an specified element from a column by **first referencing the column and
then it's index**

```py
  cities = df['city']
  index = 102               # The row index
  print(cities[index])      # Toronto
```

### Look at the first or last rows of the dataframe

You can view the first 5 rows of your dataframe with the `self.head()` method
and conversely the last 5 rows with `self.tail()`

They also accept an integer to **modify** the **number of rows** being display

```py
  df.head()
  df.tail(8)            # Display las 8 rows
```

### Create a startup options file

You can modify pandas options with `pd.set_option()` and create a script that
will run them at the start of your interpreter session

For more options you can check the [options
documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/options.html)

```py
  import pandas as pd

  def start():
      options = {
          'display': {
              'max_columns': None,
              'max_colwidth': 25,
              'expand_frame_repr': False,  # Don't wrap to multiple pages
              'max_rows': 14,
              'max_seq_items': 50,         # Max length of printed sequence
              'precision': 4,
              'show_dimensions': False
          },
          'mode': {
              'chained_assignment': None   # Controls SettingWithCopyWarning
          }
      }

      for category, option in options.items():
          for op, value in option.items():
              pd.set_option(f'{category}.{op}', value)  # Python 3.6+

  if __name__ == '__main__':
      start()
      del start  # Clean up namespace in the interpreter
```
