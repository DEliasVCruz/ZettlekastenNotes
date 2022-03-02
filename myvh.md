# lang.py.module.pandas.rows

Work with rows of a dataframe or series object

## Synopsis

```py
  row_element = df[<column>][<row>]
  entire_row = df.iloc[0]
```

## Overview

Rows are represented as `Series` object for whom the index labels represent
what would be their coulmns in a dataframe

## Cookbook

### Determine how many rows a dataframe has

When you apply the `len()` function to a dataframe you will get the number of
rows in your dataframe

```py
  len(df)               # number of rows in the dataframe
  len(df['Scores'])     # number of rows in a columns
  df['Scores'].count()  # number of rows in a columns
  df.index              # A list of al the index values
  df.index[1]           # Get the name of your second row
  max(df.index)         # maximum row index
  print(df.index)       # RangeIndex(start=0, stop=100, step=1)
```

### Get the number of rows and columns of a dataframe

You can also use the `self.shape` attribute to get the **dimensionality of the
dataframe**. This will return a tuple of rows and columns

```py
  print(df.shape)       # (rows, columns)
```

### Select specified rows by index label

You can also **access a whole row** by it's **row label** using the `loc[]`
[accessor](./4sli.md)  or `iloc[]` to reference it by it's **row**
[index](./bzog.md) **number** . If a single row is referenced **by it's label**
, then it **will return** an instance of a `series` object

```py
  df.loc[102]       # Get all the elements for each column in row labeled 102
  df.iloc[0]        # Get all the elements for each column in the first row
```

### Insert a new row to your dataframe

One way to insert a new row to your dataframe is by first creating it as an
stand alone series using the `Series` class

With the following **arguments**:

- `data`: The **data as a list** for each column of the row (**in order**)
- `index`: The **index labels** are the would be **column names**
- `name`: The **would be label** for the new **row**

**After** creating the `series` representing our new row. You can **append** the
new row to the **end of the dataframe** with the `append()` method

The `append()` method **does not perform mutation** and instead returns a new
dataframe

```py
  john = pd.Series(data=['John', 'Boston', 34, 79], index=df.columns, name=17)
  df = df.append(john)
```

### Delete a row from your dataframe

With the `drop()` method you can **delete** an **arbitrary row** by it's **row label**.

This **does not performe mutation** on your dataframe and instead return a new
dataframe object

```py
  df = df.drop(labels=[17])
```

### Locate rows conditionally

You can also use `loc[]` and pass a conditional expression [filter](./niq3.md)
for the rows

```py
  nba.loc[nba["fran_id"] == "Lakers", "team_id"].value_counts()
```

### Perform row wise operations

To get **apply** an [aggregation function](./l1ya.md) **on one or every row**
of a dataframe you need to pass the `axis="columns"` to the aggregationn function

```py
  df["Totals"] = df.sum(axis="columns")
```
