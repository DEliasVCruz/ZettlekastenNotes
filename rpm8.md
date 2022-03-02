# lang.py.module.pandas.cut

Segment and label ranges of data values into categorical bins

## Synopsis

```py
  cut_series = pd.cut(x=<series-object>,
                      bins=<list-of-ranges>,
                      include_lowest=<boolean>,
                      labels=<list-of-mappings>)[.astype(<casted-type>)]
```

## Overview

You can use `cut()` to create a `Series` object of [mappings](./oft9.md) based
on ranges called `bins`

- `bins`: A list of ranges to do the replacement on
- `labels`: The value that will replace their corresponding range

Use cut when you need to [segment](./tiqw.md) and [sort](./mfgd.md) data values
into bins

### Parameters

- `x`: A **one dimensional array like** such as a `Series` object

- `bins`: The ranges to bin on, **can accept** an:

  - **int**: Number of equal-width bins in the range of `x`
  - **list of scalars**: Defines the bin ranges as a sequence

- `right`: Wheter the right most edge is close or open

  - **Default** `True`

- `labels`: Specify the labels for the ranges of bins

  - Must be the **same length** of **resulting bin ranges**

- `include_lowest`: Whether the left most edge should be open or close

  - **Default**: `False`

## Cookbook

### Perform binning into an equal number of bins

You can replace your data for equal range intervals in which the original data
point lies on

For this just pass an [integer](./x4ok.md) to `bins` and it will represent the
number of equal range intervals

```py
  series = pd.Series(np.array([2, 4, 6, 8, 10]),
                index=['a', 'b', 'c', 'd', 'e'])
  pd.cut(x=series, bins=3)

# Results
# a    (1.992, 4.667]
# b    (1.992, 4.667]
# c    (4.667, 7.333]
# d     (7.333, 10.0]
# e     (7.333, 10.0]
```

### Perform binning into a pre-specified array of bins

You can also specify the **set of ranges for binning criteria**, by passing it
as a [list](./7cxo.md) of scalar values

By **default** the **first element** of the list won't be inclued (**will be
open**). You can change that by passing `include_lowest=True`

```py
  series = pd.Series(np.array([2, 4, 6, 8, 10]),
                index=['a', 'b', 'c', 'd', 'e'])
  pd.cut(x=series, bins=[0, 4, 7, 10], labels=['Bad', 'Medium', 'Good'])

# Results
# a    'Bad'
# b    'Bad'
# c    'Medium'
# d    'Good'
# e    'Good'
```

### Convert data from continues variable to a categorical variable

You can turn a series of continues data into a set of [categorical](./p1g8.md) labels
that will **replace and perform a mapping** based on ranges

```py
  cents_per_kwh = pd.cut(x=df.index.hour,
                         bins=[0, 7, 17, 24],
                         include_lowest=True,
                         labels=[12, 20, 28]).astype(int)

  df['cost_cents'] = cents_per_kwh * df['energy_kwh']
```
