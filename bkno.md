# lang.py.module.pandas.read

Read and import data from diferent formats and sources into a dataframe

## Synopsis

```py
  df = pd.read_<format>()
```

## Overview

You can import data from external sources and transform it into a dataframe
with the extructure `<dataframe-object> = pd.read_<format>(<input>)`

## Cookbook

### Read chunks of data at a time

If you are creating a dataframe from [reading](./5t4z.md) a csv, json, sql or
excell file you can pass the `chunksize` parameter and this will return an
[iterable](./p7q9.md) that will yield rows according to the chunksize

```py
  for df_chunk in pd.read_csv('data.csv', index_col=0, chunksize=8):
      print(df_chunk, end='\n\n')
      print('memory:', df_chunk.memory_usage().sum(), 'bytes',
            end='\n\n\n')
```

### Create a dataframe from a CSV file

You can create a dataframe from a [csv](./rlaw.md) file with the `read_csv()`
function.

- `index_col=0`: **If** your csv file has the **first column** as the **index labels**
- `parse_dates=[<column-name>]`: Specify the values of column are dates
- `sep=<string>`: What is the column separator character
- `chunksize=<int>`: The amount of rows to read at a time
- `header=<int>`: The 0 index line that will serve as the header
- `usecols=[<list-of-cols]`: The columns you want to use
  - It also uses 0 based index, 0 being the index column
- `na_values=<string>`: Specify other labels for missing values
  - By default `''` is treated as a missing value
  - It will replace them with `NaN`

```py
  df_csv = pd.read_csv("<csv_file.csv>", index_col=0, parse_dates=['DATES'], sep='|')
```

### Create a datraframe from an excel file

You will also **need one** of this libraries **installed**:

- [openpyxl](https://openpyxl.readthedocs.io/en/stable/)
- [xlrd](https://xlrd.readthedocs.io/en/latest/)

Some **usefull parameters** are:

- `sheet_name`: The name or 0 based index of the sheet to read from
- `parse_dates=[<column-name>]`: Specify the values of column are dates
  - It also uses 0 based index, 0 being the index column
- `usecols=[<list-of-cols]`: The columns you want to use

```py
  df_csv = pd.read_excel("<excel_file.xlsx>"[,index_col=0, usecols=[0, 1, 2]])
```

### Create a dataframe from a sql query
