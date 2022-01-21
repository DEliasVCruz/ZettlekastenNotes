# lang.py.module.pandas.iterate

Ways to iterate over a pandas dataframe

## Synopsis

```py
  for [col|row]_label, [col|row] in df.iter[items|rows|tuples]:
    (...)
```

## Overview

You can [iterate](./p7q9.md) over columns and rows in your dataframe with **speciallized
methods**. All of them [yield](./4g9v.md) **a tuple** for each iteration

- `iteritems()`:
  - **Iterate** over the **columns** of your dataframe
  - **Yields** the **column label** and the **column data as** a `Series` object
- `iterrows()`:
  - **Iterate** over the **rows** of your dataframe
  - **Yields** the **row label** and the **row data as** a `Series` object
- `itertuples()`:
  - **Iterate** over the **rows** of your dataframe
  - Yields a named tuple
  - `name=`(**string**): Changes the name of the tuple (**default**: Pandas)
  - `index=`(**boolean**): Include row labels (**default**: `True`)

## Cookbook

### Iterate over the rows or columns

You can iterate over the columns of a dataframe with `iteritems()`

```py
  for col_label, col in df.iteritems():
      print(col_label, col, sep='\n', end='\n\n')
```

You can iterate over the columns of a dataframe with `iterrows()`

```py
  for row_label, row in df.iterrows():
      print(row_label, row, sep='\n', end='\n\n')
```

### Create named tuples from the rows

You can create named tuples from the rows in your dataframe. This is **usefull
for creating** [objects](./unhs.md) **out of** your dataframe **rows**

```py
  for row in df.loc[:, ['name', 'city', 'total']].itertuples():
      print(row)

  # Pandas(Index=10, name='Xavier', city='Mexico City', total=82.3)
  # ...
```
