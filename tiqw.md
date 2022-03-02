# lang.py.module.pandas.grouping

Perform grouping similar to sql query group by

## Synopsis

```py
  df.groupby([<columns>]).<aggregation-function>()
```

## Overview

Refers to a **process where** we:

1. **Split a dataset into groups**
2. **Apply some** [aggregation](./s2s7.md) **function** to all it's elements
3. And **combine the reduced groups together**

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

### Apply a custom aggregation function

You can use a **custom function** as your **aggregation function** with either:

- [apply()](./j4nr.md): Perform **any operation** and get a new indexing (**slowest**)
- [agg()](./s2s7.md): **Aggregate** groups and get **groups as the new index**
- [transform()](./f2vu.md): Do some operation **without altering the original indexing**

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

When you group by more than one column the resulting [index](./271q.md) is a **hierarchical
index** to change the names of this use the `rename_axis()` method

```py
  df.groupby([df.index.year, df.index.quarter])["co"].agg(
        ["max", "min"]
      ).rename_axis(["year", "quarter"])
```

### Emulate a pivot table behaviour (tabla dinamica)

You can emulate the behaviour of a [pivot table](./spn7.md) with the
`unstack()` [index stacking](./tahi.md) method

- Using `groupby` is **faster** than `pivot_table` but **less idiomatic**

- By default when you group by more than one column, they become a
  **hierarchical index**.

- In a pivot table you want one of the columns to
  be the index and the other the column of your pivot table

That's why you use `unstack()` that by **default** will **turn** the **socond
group by** column **into** the **column** of your **pivto table**

- `fill_value`: What **value to use if** a value is **not found** for the
  combination of row column

```py
  df.groupby(['Station', 'Year'])['Sales'].sum().unstack(fill_value=np.nan)
```

### Change the grouping fields as regular columns

By **default** the **values** of the **group** columns becomes a **hierarchical index**
label.

To **force** use a **numerical index** and have the group fields as new
**regular columns** in your dataframe, use the `as_index=False` argument

- This **most** closely **mimics** the result of an `sql` **group by**
- The **new index defaults** to a `RangeIndex`

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

### Iterate over group by groups

You can [iterate](./p7q9.md) over a group by object and it will **return** a
**tuple** of the **group label** and the **group dataframe**

```py
  for group, table in grouped:
    print(group)
    print(table, end='\n\n')
```

### Get a group by it's group name

When you create a group object you **can use** the following **methods**:

- `groups.keys()`: Get then names of the group labels
- `get_group()`: Get a group dataframe from the group name

```py
  grouped = df.groupby('Gender')
  grouped.groups.keys()                     # dict_keys(['M', 'F'])
  male_group  = grouped.get_group('M')
```
