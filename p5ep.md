# lang.py.module.sql.pony.aggregation

Working with query agregations in your Pony database

## Synopsis

```py
  <agregation>(<comprehension-like-query>)
```

## Overview

You can read more about it [here](https://docs.ponyorm.org/aggregations.html)

## Cookbook

### Use agregation functions as queries

You can use various agregation functions and pass a [comprehension](./7lub.md) like
expression of a [collection set](./0n1h.md) or [entity table](./6p3h.md)

- This will apply inmediate agregation to [query](./ca6a.md) structures

```p
  count(s for s in Student if s.group.number == 101)
```

### Get an agregation count

You can use agregation to **display something like** you would **normally get**
in [sql agregation](./6mxs.md)

- You need to make the result a [tuple](./hsr4.md)

```py
  select((g, count(g.students)) for g in Group if g.dept.number == 44)
```
