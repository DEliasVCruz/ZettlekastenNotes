# lang.py.module.pandas.visualization

Create visualizations of your dataframe with pandas

## Synopsis

```py
  df.plot(kind=<plot-type>[, <extra-argmunts>])
```

## Overview

[Pandas](./czyt.md) includes some **built-in visualization tools** to integrate
with your [dataframes](./5t4z.md)

There are **different** kind of **plotting options** that you can supply to the
`kind` argument:

- `line`: Create a line plot
- `bar`: Create a bar plot
- `pie`: Create a pie chart

### Arguments

You can **customize** your **plot figure** by passing this arguments:

- `kind`: The type of plot
- `ax`: Define a custom [pyplot](./3s1w.md) axis to use
- `xlabel`: The string to display as the **x axis label**
- `ylabel`: The string to display as the **y axis label**
- `title`: The string to display as the **title of the figure**
- `figsize`: A [tuple](./hsr4.md) with the **size of the figure** `(x, y)`

## Cookbook

### Use a custom pyplot figure

You can provide your own `pyplot` figure and axis to display your `dataframe`
and thus have more granuality on it's display

For this you need to pass the `axis` to the `ax` parameter. And the operate on
`ax` and `fig` as a normal `pyplot` figure

```py
  import matplotlib.pyplot as plt

  fig, ax = plt.subplots(figsize=(10, 6))
  df.plot(ax=ax, kind='bar')

  ax.set_xlable('My X label')
  ax.set_ylable('My Y label')

  fig.suptitle('My Custom Visualization')

  fig.show()
```

### Create a line plot figure

To create a line plot figure use the `line` plot type

```py
  df.plot(kind='line', xlabel='Year', ylabel='Population',
          title='Population (1955-2020)'
          figsize=(8, 4))
```

### Create a bar plot figure

You can create a bar plot with the `bar` plot type. Remember that when we
create bar plots, we are matching indices against values, so we must **have what
we expect to be our x axis as the index in our dataframe**

```py
  df.plot(kind='bar', color='orange',
          xlabel='Year', ylabel='Population',
          title='Population 2020')
```

### Create a bar plot with multiple adjacent labels

If you want to have **multiple labels along side each other**, each for a
single **corresponding x axis**, you can do it by forming the **bar plot from a
dataframe with multiple columns**

**Each column** is going to be **one** of our **labels**, the **index** is
going to be our **x axis** and our **y axis** is going to be their
**corresponding table value**

```py
  df_multiple = df[df.index.isin([1980, 1990, 2000, 2010, 2020])]
  df_multiple.plot(kind='bar', color='orange',
                   xlabel='Year', ylabel='Population',
                   title='Population 2020')
```

### Create a pie chart

A pie chart follows the same logic that a bar plot, here **each index (row)**
will be **a piece of our pie chart** and the **data** will be the **column**.
So we will have **one column and several rows**.

The `y` argument **indicates** the **column** that will be **taken as the data**

```py
  df.plot(kind='pie', y='2020', title='Population in 2020(%)')
```

### Save a pandas plot as a jpg png file

To **save a generated plot as a png** file we will need the
[matplotlib](./3s1w.md) library and use the `savefig()` function

```py
  import matplotlib.pyplot as plt

  df.plot(kind='line', xlabel='Year', ylabel='Population',
          title='Population (1955-2020)'
          figsize=(8, 4))

  plt.savefig('my_plot.png')
  plt.show()
```
