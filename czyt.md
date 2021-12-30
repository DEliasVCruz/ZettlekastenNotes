# lang.py.module.pandas

Work with structured data like tables

## Synopsis

```py
  import pandas as pd
```

## Overview

The pandas module allows us to work with structured data like tables with a
special type called a data grame

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

### Display all columns, amount of not-nulls and their data types

You can display a list of all the columns in your dataframe and the type of
data thy hold. This will **also show** you **the amount of not-null** records in
each column

```py
  df.info()
```

### Display general statistic summary

If you want a **small sumary** with some **basic statistic analisis** of your
**dataframe** you can use the `describe()` method

This **will show** you:

- **Count**: How many rows each column has
- **Mean**: The avarage of the values in the field
- **Standard Deviation**: The difference from the mean
- **Min**: The minimum value in the field
- **Max**: The maximum value in the field
- **Percentails**: The 25%, 50% and 75% percentails from the mean

```py
  df.describe()
```

By **default**, `describe` will only perform statistic **analysis** on fields
of **numeric value**. With the `include=object` argument it will also display
statistic analysis **for non numberic values**

This will **also show**:

- **Unique**: How many unique values there are
- **Top**: The most repeated value

```py
  df.describe(include=object)
```

### Determine how many rows a dataframe has

When you apply the `len()` function to a dataframe you will get the number of
rows in your dataframe

You can also use the `self.shape` attribute to get the **dimensionality of the
dataframe**. This will return a tuple of rows and columns

```py
  len(df)               # number of rows in the dataframe
  len(df['Scores'])     # number of rows in a columns
  df['Scores'].count()  # number of rows in a columns
  df.index              # A list of al the index values
  max(df.index)         # maximum row index
  print(df.index)       # RangeIndex(start=0, stop=100, step=1)
  print(df.shape)       # (rows, columns)
```

### Get the name of the columns and their datatypes

You can know the name of your **fields** (columns) with the `columns` atribute

```py
  print(df.columns)
```

You can also get the **data type** of the elements in each colummn with a small
sumary with the `dtypes` attribute

```py
  print(df.dtypes)
```

### Select a column from your dataframe

You can reference and **select fields** from your dataframe **like elements**
in a [dictionary](./0loj.md) this will **return** a **series** object

```py
  print(df_exams['Gender'])     # Print the series from the field "Gender"
```

You can **use most attributes** from a **dataframe with series** too:

- `df_exams['Gender'].index`: List every index
- `df_exams['Gender'].head(8)`: Display the first 8 rows

### Select more than one column at once

To **select more than one column** you need to reference them in a
[list](./7cxo.md). This **returns another dataframe** object

The **order** in which you pass the **fields in the list** is the **order** in
which they **will appear** in the dataframe

```py
  print(df_exams[['Gender', 'Math Score']])    # Print a dataframe with the 2 fields
```

### Select specified rows by index

You can **select and display** only the **rows that match** a certain in
**index** with the `index.isin()` method and **reference** it for the dataframe

```py
  df[df.index.isin([2017, 2018, 2019, 2020])]
```

### Transpose a dataframe

If you want to **interchange rows for columns** you can use the `T` attribute.
This returns a new transposed dataframe, it **does not perform mutation**

```py
  print(df.T)       # Transposed dataframe
```

### Look at the first or last rows of the dataframe

You can view the first 5 rows of your dataframe with the `self.head()` method
and conversely the last 5 rows with `self.tail()`

They also accept an integer to **modify** the **number of rows** being display

```py
  df.head()
  df.tail(8)            # Display las 8 rows
```

### Drop null values from a dataframe

When **performing clean up** on your dadtaframe, you may want to **remove any row
that has null values**. For that we use the `dropna()` method

It **returns a new dataframe**, if you want to **mutate** your **original**
dataframe **use** the `inplace=True` argument or re assign it to the original
dataframe

```py
  df_population = df_population_raw.dropna()
```
