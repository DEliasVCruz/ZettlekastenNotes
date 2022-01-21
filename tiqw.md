# lang.py.module.pandas.grouping

Perform grouping similar to sql query group by

## Synopsis

```py
  df.groupby([<columns>]).<aggregation-function>()
```

## Overview

Refers to a process where we split a dataset into groups, apply some function
(typically aggregation) , and then combine the groups together.

Keep in mind that you could **achieve something similar** with
[pivot](./spn7.md) tables

### More information

You can find more information in the **official resources**

- [Cookbook](https://pandas.pydata.org/pandas-docs/stable/user_guide/cookbook.html#cookbook-grouping)
- [User Guide](https://pandas.pydata.org/pandas-docs/stable/user_guide/groupby.html)
- [Methods](https://pandas.pydata.org/pandas-docs/stable/reference/groupby.html)

## Cookbook

### Group by a column and count

For this you first pass the name of the column to group by and then use the
`size()` method to perform counting

- Using this method of aggregation **does not excludes** `NaN` values **from
  it's calculation**

```py
  tips.groupby('sex').size()
```

This is all **similar to** the following [sql](./6mxs.md) query

```sql
  SELECT sex, count(*)
  FROM tips
  GROUP BY sex;
```

### Group by and use aggregations methods

You could also use the `count()` method but you'll have to **specify the column**
or columns to count. Otherwise it will apply it for every column

- Using this method of aggregation **excludes** `NaN` values **from it's calculation**

This is also needed to apply this for **other aggregation functions**:

```py
  tips.groupby('sex')['total_bill'].count()
  tips.groupby('sex')['total_bill'].sum()
  tips.groupby('sex')['total_bill'].min()
```

### Use more than one aggregation function

You can use more than one aggregation function on **more than one column** with
`agg`. It comes in the form of a [dictionary](./0loj.md) where:

- **keys**: The column name
- **values**: Calable functions
  - It can have **more than one function** in the form of a [list](./7cxo.md)
  - This is usefull if you want to use the different functions on the same column

```py
  tips.groupby('day').agg({'tip': np.mean, 'day': np.size}
```

This is all **similar to** the following `sql` query

```sql
  SELECT day, AVG(tip), COUNT(day)
  FROM tips
  GROUP BY day;
```

It can also accept a single [list](./7cxo.md) in which case it will apply evry
one of the agregation functions to each selected column

```py
  tips.groupby('day')['tip'].agg(["mean", "count"])
```

### Apply a custom aggregation function

You can use a **custom function** as your **aggregator function** with
`apply()`. Keep in mind that this **can be a slow operation**, and if posible
try to avoid it.

```py
  df.groupby("outlet", sort=False)["title"].apply(
      lambda ser: ser.str.contains("Fed").sum()
  ).nlargest(10)
```

### Group on more than one column

To group by more than one column pass the names as a list. The **group order**
will be determined by the **order of** the **columns in** the **list**

```py
  tips.groupby(['smoker', 'day']).agg({'tip': [np.size, np.mean]})
```

This is all **similar to** the following `sql` query

```sql
  SELECT smoker, day, COUNT(tip), AVG(tip)
  FROM tips
  GROUP BY smoker, day;
```

### Rename the index of multiple column group by

When you group by more than one column the resulting index is a **hierarchical
index** to change the names of this use the `rename_axis()` method

```py
  df.groupby([df.index.year, df.index.quarter])["co"].agg(
        ["max", "min"]
      ).rename_axis(["year", "quarter"])
```

### Make the grouping fields as regular columns

By **default** the **values** of the **group** columns becomes a **hierarchical index**
label.

To **force** use a **numerical index** and have the group fields as new
**regular columns** in your dataframe, use the `as_index=False` argument

- This **most** closely **mimics** the result of an `sql` **group by**

```py
  df.groupby(["state", "gender"], as_index=False)["last_name"].count()
```

### Group by any array like

You can use any **array like** such as that represents a sequence of labels on
which to perform the grouping and splitting

```py
  day_names = df.index.day_name()
  df.groupby(day_names)["Temperature"].mean()
```

This sequence of labels **does not need to match** or be part of the **columns
of** the **dataframe**, is **just** has to have the **same number of rows as**
the columns you are **aggregating**

```py
  mentions_fed = df["title"].str.contains("Fed")   # Series of booleans

  mentions_fed.shape                               # (422419,)
  df["outlet"].shape                               # (422419,)

  mentions_fed.groupby(
     df["outlet"], sort=False
     ).sum().nlargest(10).astype(np.uintc)
```
