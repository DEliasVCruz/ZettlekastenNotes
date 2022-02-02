# lang.py.data.bool

Represents true or false

## Overview

In python they reperesent **condition test statements**, since they are most
used in **conditional operations**

- `True`
- `False`

### Cookbook

### What defines a truthy and falsy

In python every number other than `0` constitutes a **thruty** meaning they
will **pass a conditional test** just like `True` would

On the other hand a `0` constitute a falsie and will **fail a conditional
test**, just like `False` would

### Turn a thruthy or falsy into a boolean

You can turn **tests, falsies, thruties** into a `True` or `False` boolean with
the built-in `bool(<text>)`

```py
  def is_multiple(number, multiple):
    return not bool(number % multiple)
```
