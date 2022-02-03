# lang.py.oper.classes.built_functions

There are some built in functions to operate on classes and their attributes

## Synopsis

```py
  [get|del|has|set]attr(<object>, <attribute>[, [<default>|<value>]])
```

## Overview

`Python` has some built-in functions to operate on the attributes of an
instance of a [class](./unhs.md)

- `getattr()`: Get the value of an attribute
- `setattr()`: Change the value of an attribute
- `hasattr()`: Check if the attribute exists
- `delattr()`: Remove an attribute

## Cookbook

### Get the value of an attribute

It accepts **three arguments**:

- `object`: The instance
- `attribute`: The searched attribute
- `default`: What to return if the attribute does not exists

```py
  class Person:
    name = "John"
    age = 36
    country = "Norway"

  x = getattr(Person, 'page', 'my message')
  print(x)                                      # my message
```

### Find if an object is an instance of a class

You can us the `isisntance()` function to find if an object is an instance of a
class. This is better than using the `type()` function

```py
  obj = 12
  if isinstance(obj, int):
      print(f'{obj} is an integer')
```
