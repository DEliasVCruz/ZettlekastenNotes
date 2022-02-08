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

- `index_col=<col-name>`: Indicate what column values should be taken as the index
- `parse_dates=[<column-name>]`: Specify the values of column are dates
- `sep=<string>`: What is the column separator character
- `chunksize=<int>`: The amount of rows to read at a time
- `header=<int>`: The `zero-index` line that will serve as the header
- `names=<list>`: A [list](./7cxo.md) of names that will serve as column names
- `converters=<dictionary>`: Do some pre-processing on the columns as `Series` object
  - Takes a dicttionary where the keys are the columns and the values the operations
- `usecols=[<list-of-cols]`: The columns you want to use
  - It also uses 0 based index, 0 being the index column
  - It can accept a function with one argument (**the column name**)
- `na_values=<string>`: Specify other labels for missing values
  - By default `''` is treated as a missing value
  - It will replace them with `NaN`

```py
  df_csv = pd.read_csv("<csv_file.csv>", index_col=0, parse_dates=['DATES'], sep='|')
```

### Preprocess column at read time

You can use the `converters` argument to do some [operation](./l1ya.md) on
individual columns as `Series` objects

It will take a [dictionary](./0loj.md) where:

- **Keys**: The name of the columns
- **Values**: The `Series` operation to do on the column

```py
  conversions = {'Name': str.lower, 'Last Name': str.lower}
  csv_df = pd.read_csv("my.csv", converters=conversions)
```

### Select columns to read conditionaly

You **can pass** a **function** to `usecols` that:

- Will **take** only **one argument**: the **column name**
- **If** the function **returns true** then the **column is included**

**In this example** it will check if the string `'Submission'` is part of the
column name and included if it's not

```py
  csv_df = pd.read_csv('my.csv', usecols=lambda x: "Submission" not in x)
```

### Specify datetime columns at read time

You can use the arguments:

- `parse_dates=[<column-name>]`: Specify the values of column are dates
- `date_parser=<function>`: A function that turn the values into `datetime` formats

```py
  csv_df = pd.read_csv('my.csv', parse_dates=['Dates'])
```

### Parse various columns as one datetime column

You can specify various columns as one single column that will be of `datetime` type

- `[[<date-col>, <date-col>]]`: Combine both columns and parse as single date column
- `{<col-name>: [<date-col>, <date-col>]}`: Parse cols and call result as the key

```py
  csv_df = pd.read_csv('my.csv', parse_dates=[{'Date': [1, 2]}])
```

### Create a datraframe from an excel file

You will also **need** the [openpyxl](./whkz.md) library **installed**:

- Some **usefull parameters** are:

  - `sheet_name`: The name or 0 based index of the sheet to read from
  - `parse_dates=[<column-name>]`: Specify the values of column are dates
    - It also uses 0 based index, 0 being the index column
  - `usecols=[<list-of-cols]`: The columns you want to use

```py
  df_csv = pd.read_excel("<excel_file.xlsx>"[,index_col=0, usecols=[0, 1, 2]])
```

### Create a dataframe from a sql query

### Create a dataframe from the clipboard

You can create a datframe **directly from** the clipboard **data buffer** with `read_clipboard`

- `na_values=<string>`: Specify other labels for missing values
- `parse_dates=[<column-name>]`: Specify the values of column are dates

```py
# AFter having copy a dataframe like structure into the clipboard
  clipboard_df = pd.read_clipboard()
```
