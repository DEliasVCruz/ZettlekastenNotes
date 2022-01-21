# lang.py.module.pandas.applymap

Map a calable function to every element in your dataframe

## Synopsis

```py
  def custom_calable(item):
      ...

  df = df.applymap(custom_calable)
```

## Overview

You can use `applymap` like the built in [map](./kqas.md) function and it will
apply the custom function to every element (**every individual cel**) in your
dataframe and **replace** it **with** the **returned output**

Keep in mind that this **can have significant runtime** for larger datasets.
Try to apply **vectorized operations** wherever posible instead

## Cookbook

### Operate on every item of a dataframe

Just create a function that **takes** a **single element** from the dataframe
and **returns** a **single operated element**

```py
  def get_citystate(item):
      if ' (' in item:
          return item[:item.find(' (')]
      elif '[' in item:
          return item[:item.find('[')]
      else:
          return item

  towns_df =  towns_df.applymap(get_citystate)
```
