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
- **Agg**: Use **more than one aggregation function** and returns it's results

You could also get a [summaries version](./czyt.md) of all this with `describe()`

```py
  df_exams['Math Scores'].sum()                     # Sum all the rows
  df_exams['Math Scores'].count()                   # Count the number of rows
  df_exams['Math Scores'].mean()                    # Find the average value
  df_exams['Math Scores'].std()                     # Find the standard deviation
  df_exams['Math Scores'].min()                     # Find the minimum value
  df_exams['Math Scores'].max()                     # Find the maximum value
  df_exams['Math Scores'].agg(("min", "max"))       # Find the min and max value
```

**Calling** this methods **directly on** your **dataframe** will **return** a
`series` object with the **result for each column**

```py
  df_exams.mean()   # Series object with the mean value of each column
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

### Find the number of unique values in a field

You can get the number of unique values in a field with the `nunique()` method.

If you have a large ratio of total values to unique values, that field is a
good candidate for [categorical](./p1g8.md) data type

```py
  df["Gender"].nunique()    # 2
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

### Turn string values into numeric values

You can transform a column that has **values represented as strings into** one
of **numeric type** with the `to_numeric()` function

```py
  df["Grades"] = pd.to_numeric(df["Grades"])
```

### Use numpy functions for operations

You can use [numpy](./5nfr.md) functions and **pass parts of** your
[pandas](./czyt.md) **dataframe with** the `iloc[]` [accessor](./unhs.md)
instead of a numpy array

**In this example** to calculate the **weighted average of three columns for
each row** we use the `np.average()` function with the `axis=1` argument

```py
  scores = df.iloc[:, 2:5]
  df['total'] = np.average(scores, axis=1, weights=[0.4, 0.3, 0.3])
```

This will be the **same as**:

```py
  df['total'] = 0.4 * df['py-score'] + 0.3 * df['django-score'] + 0.3 * df['js-score']
```

### Perform rolling window operations

Sometimes you may want to perform operations were you **operate on a set of
values in a window** and this window **moves as we traverse the elements** in
our series

You can do this with the `rolling()` method that **creates a fixed size window**
that moves across by each element in your `Series`

**At the beginning only the end of the window** will be positioned on the first
value and more of it will be moving inside the `Series` accordingly

It will **not perform operations unless it has all values** that **correspond
to** the **size** of the **window**. You **can specify** a number of **minimum
values** it needs with the `min_periods` argument

```py
  df = pd.DataFrame({'B': [0, 1, 2, np.nan, 4]})
  df.rolling(window=2, min_periods=1).sum()         # Operate with at least one value
```
