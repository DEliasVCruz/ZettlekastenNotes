# lang.py.module.pandas.operations

You can perform different operations with the values of your dataframe

## Synopsis

```py
  df[<field>].<operation>()
```

## Overview

You can **perform** different **operations** on the fields of your [dataframe](./5t4z.md)

- **Sum fields** between each other
- Calculate **aggregated values** of a field

## Cookbook

### Calculate total field values

You can perform agregated operations on the values of a column. Such operations
can be:

- **Sum**: Sum all the values in a field
- **Count**: Count the number of rows in a field
- **Mean**: Calculate the mean value of a field
- **Std**: Calculate the standard deviation of a field
- **Max**: Find the maximum value in a field
- **Min** : Find the minimum value in a field

You could also get a [summaries version](./czyt.md) of all this with the `describe()`

```py
  df_exams['Math Scores'].sum()     # Sum all the rows
  df_exams['Math Scores'].count()   # Count the number of rows
  df_exams['Math Scores'].mean()    # Find the average value
  df_exams['Math Scores'].std()     # Find the standard deviation
  df_exams['Math Scores'].min()     # Find the minimum value
  df_exams['Math Scores'].max()     # Find the maximum value
```

### Perform operations between fields

If you wanted to perform **operations between** all the **values of more than
one field** you can do it by **referencing each column** by their name **and
doing** your basic **math operations** like you would normally would

In this case we want **the average value for each row of two selected column**

```py
  df_exams['Avg Score'] = (df_exams['Lang Score'] + df_exams['Math Score']) / 2
  df_exams.round(2)
```

### Count based on value repetition

If you want to **count** so as to get the **amount of times each distinct
value** in a field **is repeated**, you can use the `value_counts()` method

```py
  df_exams['Gender'].value_counts()

# Output
  female: 518
  male:   482
```

### Get the percentage that each value in a field represents (relative frequency)

If you want to **get the relative frequency** of each value in the field, the
**percentage that it represents** from the total of values. Then you can pass the
`normalize=True` argument to `value_counts()`

```py
  df_exams['Gender'].value_counts(normalize=True)

# Output
  female: 0.518
  male:   0.482
```
