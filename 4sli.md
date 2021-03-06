# lang.py.module.pandas.accessors

Extract elements, rows or columns by indices

## Synopsis

```py
  df.<accessor>[<rows>, <columns>]
```

## Overview

You can get elements, rows or columns by using accessor that will reference
them by rows and columns

### Accessors

Pandas defines 4 [accessors](./unhs.md) to **select rows or columns** from your
dataframe as a `series` or a `dataframe`

You **can use** the following accessros **to retrieve rows or columns**:

- `loc[]`: Retrieves a row or column **referenced by** it's **label**
- `iloc[]`: Retrieve a row or column **referenced by** it's **index number**
  - It also **supports negative indices** to access from the last element
- `at[]`: Takes the **labels of rows and columns** and **returns a single data value**
- `iat[]`: Takes the **indices of rows and columns** and **returns a data value**
  - You can use it as `Excell`'s `coincidir()` function

The `loc[]` and `iloc[]` accessors **support** [slicing](./7cxo.md)

## Cookbook

### Select columns and rows using accessors

Each element (`<rows>` and `<columns>`) **supports passing** either a **slice** or
a **list/array** alongside each other. **When** you pass a **slice on** a **label
reference** both sides of the slice are **inclusive**

```py
  df.loc[:, 'city']     # Get all the rows from the city column
```

In this **example** we **select rows 2 to 5 from the first and second column**:

```py
  df.loc[11:15, ['name', 'city']]   # Referenced by label
  df.iloc[1:6, [0, 1]]              # Referenced by index number
```

### Get a single element from a column and row intersection

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

### Use conditional boolean expressions inside accessors

You can use **conditional expression** to will operate as [filters](./niq3.md)
**inside** your accessor.

Since the [rows](./myvh.md) part of your accessor **can accept** any **array
like** to perform slicing

```py
  filtered_column_df = df.loc[df[<filter-column>] == "<filter-value>", "<accessed-column>"]
```

### Selecting data with accessors and `isin()`

Since the `loc` accessor can accept any array like and conditional expression
return a `Series` object of `boolean` values. We can use it to select rows

**In this example** we get the rows where the date hour is between 5 and 10 pm

```py
  df.set_index('date_time', inplace=True)

  peak_hours = df.index.hour.isin(range(5, 10))
  df.loc[peak_hours, 'average_price']
```

### Accessors of the `Series` object

The `Series` object has three distinct accessors:

- `cat`: Working with [categorical](./p1g8.md) data
- `str`: Working with values as [string](./m0jc.md) data in a vectorized way
- `dt`: Working with [datetime](./6e6x.md) values

### Locate rows or columns `zero-index` with labels

You can use the `iloc` accessor in combination with the `get_loc()` method of a
[Index](./271q.md) object to achieve the same result as `loc`

**In this example** we get the row at `zero-index` position `0` in the `py-score`
column

```py
  df.iloc[0, df.columns.get_loc('py-score')] = 13
```
