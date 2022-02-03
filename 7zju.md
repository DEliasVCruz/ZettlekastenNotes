# lang.py.oper.variable

Create reference to Python data structures or objects

## Synopsis

```py
  <variable-name> = [<data>|<object>]
```

## Overview

The standard way of working with variables in `Python` to store data or objects

## Cookbook

### Conditionally assign values to variables

You can conditionally assign values to variables by **using** an **inline**
`if` [statement](./4g9v.md)

```py
  s = 's' if len(users) > 1 else ''
  message = f'The user{s} are {users}'
```
