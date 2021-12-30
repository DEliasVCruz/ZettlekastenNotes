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
  df.index[1]           # Get the name of your second row
  max(df.index)         # maximum row index
  print(df.index)       # RangeIndex(start=0, stop=100, step=1)
  print(df.shape)       # (rows, columns)
```

### Get the name of the columns and their datatypes

You can know the name of your **fields** (columns) with the `columns` atribute.
It will **return a list of all the column names** and can then be referenced
directly with an index

Keep in mind that you **can't modify an individual element directly** with this
approach

```py
  print(df.columns)
  print(df.columns[1])      # city
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

### Select a single element of your field

Every column of a dataframe is an instance of a pandas `series` object. So you
can get an specified element from a column by **first referencing the column and
then it's index**

```py
  cities = df['city']
  index = 102               # The row index
  print(cities[index])      # Toronto
```

### Select specified rows by index label

You can also **acces a whole row** by it's **row label** using the `loc[]`
attribute or `iloc[]` to reference it by it's **row index number** . If a
single row is referenced **by it's label** , then it **will return** an
instance of a `series` object

```py
  df.loc[102]       # Get all the elements for each column in row labeled 102
  df.iloc[0]        # Get all the elements for each column in the first row
```

You can **select and display** only the **rows that match** a certain in
**index label** with the `index.isin()` method and **reference** it for the dataframe

```py
  df[df.index.isin([2017, 2018, 2019, 2020])]
```

### Select columns and rows using accessors

Pandas defines 4 [accessors](./unhs.md) to **select rows or columns** from your
dataframe as a `series` or a `dataframe`

You **can use** the following accessros **to retrieve rows or columns**:

- `loc[]`: Retrieves a row or column **referenced by** it's **label**
- `iloc[]`: Retrieve a row or column **referenced by** it's **index number**
  - It also **supports negative indices** to acces from the last element
- `at[]`: Takes the **labels of rows and columns** and **returns a single data value**
- `iat[]`: Takes the **indices of rows and columns** and **returns a data value**
  - You can use it as `Excell`'s `coincidir()` function

The `loc[]` and `iloc[]` accessors **support** [slicing](./7cxo.md)

The **basic syntax** goes like:

```py
  df.<accessor>[<rows>, <columns>]
```

Each element (`<rows>` and `<columns>`) **supports passing** either a **slice** or
a **list/array** alongside each other. **When** you pass a **slice on** a **laber
reference** both sides of the slice are **inclusive**

```py
  df.loc[:, 'city']     # Get all the rows from the city column
```

In this **example** we **select rows 2 to 5 from the first and second column**:

```py
  df.loc[11:15, ['name', 'city']]   # Referenced by label
  df.iloc[1:6, [0, 1]]              # Referenced by index number
```

To get a **single value** from a **pair** of **row and column** it's best to
use the `at[]` and `iat[]` accessors

```py
# Referenced by label
  df.at[12, 'name']                 # Ana

# Referenced by index number
  df.iat[2, 0]                      # Ana
```

### Modify data with accessors

After **selecting** parts of your dataframe **with** any **accessor** you can
then **pass new values** to modify the existing ones

**In this example** we are modifying from the column with label 'py-score' every
row until the row with the label '13' with values from a list and the rest of
the rows with value 0

```py
  df.loc[:13, 'py-score'] = [40, 50, 60, 70]
  df.loc[14:, 'py-score'] = 0
```

### Extract data as a numpy array

Sometimes you may want to **extract data** from your dataframe **as a list without
it's labels**, just the data. For that you can use the `to_numpy()` method, that
will return a [numpy](./5nfr.md) **array of just the data without the column
names or index names**

The `to_numpy()` is the same as `values()` with the **added functionality** of
specifying the **optional arguments**:

- `dtype`: Set to [None](./y624.md) by default. Serves to **specify the type of
  the resulting array**
- `copy`: A [boolean](./6auy.md) for which
  - `False`: The data is tied to the dataframe and changes accordingly
  - `True`: Make a new copy detach from the origianl dataframe

```py
  df.to_numpy()
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
