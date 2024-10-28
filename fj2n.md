# lang.py.module.pandas.joining

Join dataframes based on a common key

## Synopsis

```py
  pd.merge(<left-df>, <right-df>, on=<column>, how=[left|right|outer])
```

## Overview

You can perform operations similar to [table joining in sql](./qjl9.md) with
the `merge()` method

## Cookbook

### Join to dataframes

By **default** it will perform an **inner join**. You define the join column
with the `on` parameter

```py
  pd.merge(df1, df2, on='key')
```

This is **similar to** the following `sql` query:

```sql
  SELECT *
  FROM df1
  INNER JOIN df2
    ON df1.key = df2.key;
```

### Join on a different direction

You can perform joins to different directions with the `how` argument:

- `left`: Left join
- `right`: Right join
- `outer`: Outer join

```py
  pd.merge(df1, df2, on='key', how='left')
```

This is **similar to** the following `sql` query:

```py
  SELECT *
  FROM df1
  LEFT JOIN df2
    ON df1.key = df2.key;
```

### Join on more than one column

You can join on more than one column that are present in both dataframes by
passing a [list](./7cxo.md) to `on`

```py
  inner_merged_total = pd.merge(climate_temp, climate_precip, on=["STATION", "DATE"])
```

### Join on columns that are not in each dataframe

Sometimes you may want to perform merge on **columns** that **don't have** the
**same name** on **both dataframes** for this you can use:

- `left_on`: The column from the left dataframe to merge on
- `right_on`: The column from the right dataframe to merge on

```py
  pd.merge(df1, df2, left_on="Names", right_on="First")
```

### Join on the index of a dataframe

You can also use the index of a dataframe as the column to merge on:

- `left_index`: Boolean `True` or default `False`
- `right_index`: Boolean `True` or default `False`

In which case you will have to also specify the column or index from the
opposit dataframe to join on

```py
  pd.merge(df1, df2, left_on="ID", right_index=True)
```

### Perform union on dataframes

You can unite dataframes horizontally similar to the [union in sql](./c76a.md)
with the `concat()` method

By default `concat()` works like `UNION ALL` where it just appends the second
dataframe to the first without removing duplicates

```py
  pd.concat([df1, df2], sort=False)
```

This is **similar to** the following `sql` query:

```sql
  SELECT city, rank
  FROM df1
  UNION ALL
  SELECT city, rank
  FROM df2;
```

### Remove duplicates when doing union

To achieve a behavior similar to `UNION` and remove duplicates when
performming the union use the `drop_duplicates()` method

```py
  pd.concat([df1, df2], sort=False).drop_duplicates()
```

This is **similar to** the following `sql` query:

```sql
  SELECT city, rank
  FROM df1
  UNION
  SELECT city, rank
  FROM df2;
```

### Perform vertical union of dataframes

The dafault behaviour of `concat()` is to union dataframe one on top of the
other.

But you can also union them along side eachother and increase the number of
columns with `axis="columns"`

```py
  concatenated = pandas.concat([df1, df2], axis="columns")
```

### Drop columns or rows with NaN values after union

You can use the `join="inner"` parameter to get rid of rows or columns that
upon union result in misssing values

```py
  inner_joined = pd.concat([climate_temp, climate_precip], join="inner")
```

### Start with a fresh `zero-index` after union

When performing union by default the original index label for each row will be
preserve from their original dataframe. To start the new dataframe with new 0
index use the `ignore_index=True` parameter

```py
  reindexed = pd.concat([precip_one_station, precip_one_station], ignore_index=True)
```

### Do a v-lookup styled operation

It's common when working with `excel` to do `v-lookup` (buscarv) operations
between different sets of data

For example you have a big table with some ids, and then you have some other
table with possibly matching id's and their own set of values

You may want to get some of the columns of that other table into your
big table but matching their respective row index by id

You can use the `merge` method to accomplish this sort of functionality

```py
import pandas as pd

df = pd.read_csv('data1.csv', index_col='id')
print(df)

# Output
id   size qty
3237   xl   7
3859   xl  61
3518   sm  83

refs = pd.read_csv('refs.csv', index_col='id')
print(refs)

# Output
id   reference
3859   Y328sdf
3518   Y234mds
3237   Y983msr

merged = df.merge(refs, how='left', on='id')
print(merged)

# Output
id   size qty reference
3237   xl   7   Y983msr
3859   xl  61   Y328sdf
3518   sm  83   Y234mds
```
