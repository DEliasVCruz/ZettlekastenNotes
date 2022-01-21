# lang.py.module.pandas.pivot

Create a pivot table from your dataframe

## synopsis

```py
  df.pivot(index=<columns>, colummns=<columns>, values=<values>)
```

## Overview

A pivot table **takes three columns** and **returns** a new **double entry**
[dataframe](./5t4z.md) with the two first columns as it's index and columns

There are **two main methods** to work with pivot tables:

- `pivot()`: Only creates a pivot table and does not support value aggregation
- `pivot_table()`: Creates a pivot table that supports value aggregation

You can picture this as a **dynamic table** in `excel` where the `pivot_table` method
serves as the sidebar where you constructed the dynamic table by arraying the
rows, columns and aggregated values

- You could also get a **similar result** for less complex cases using [group
  by](./tiqw.md) method similar to the `group by` from [sql](./6mxs.md)

## Cookbook

### Create a pivot table

To create a pivot table **without aggregation of values** you can use the
`pivot()` method. It will work exactly like an `Excel` **dynamic table** but
it **will not aggregate the values in the table** it will **only mapped them
in** the **double entry table**

```py
  import pandas as pd

  df_gdp = pd.read_csv('gdp.csv')
  df_gdp_pivot = df_gdp.pivot(index='year', columns='country', values='gdppc')
  print(df_gdp_pivot)

# Output

# A dataframe of years as rows and
# countries as columns with
# thier corresponding gdp per capita
# per year and country
```

### Create a pivot table with aggregated values

For this we use the `pivot_table()` method and we add a new argument `aggfunc`
that is the **aggregation function** to be performed on the values. It is
**passed as a string** and the most common is `sum` this function it **will
only aggregate numeric values**

```py
  import pandas as pd

  df_sales = pd.read_excel('sales.xlsx')
  df_sales.pivot_table(index='Gender',
                       columns='Product line',
                       values='Total',
                       aggfunc='sum')

# Output

# A dynamic table like dataframe displaying how much
# each gender spent on each product line
```

You can also create a **pivot table with only rows and aggregated values**

```py
  import pandas as pd

  df_sales = pd.read_excel('sales.xlsx')
  df_sales.pivot_table(index='Gender', values=['Quantity', 'Total'], aggfunc='sum')
```
