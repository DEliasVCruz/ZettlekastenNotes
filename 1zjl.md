# lang.py.syntax.function.arguments

You can define arguments of a function in various ways

## Synopsis

```py
  def my_func([<required_args>][, *args][, <default_args>][, **kwargs]):
      pass
```

## Overview

When working with functions you can define arguments that it will take and
operate on.

When combining required and default arguments **all** the **required
arguments** definitions **come first of** any **default argument** definition

## Cookbook

### Add a default value for an argument

A **default value** for a parameter can **prevent error** if the function is called
**without** passing **all** of the **required arguments**

To achieve this just add an `=` to the end of the **argument definition** with
the desired **default value**

```py
  def number_to_the_power_of_default(number_one, number_two=2):
    """Raise a number to an arbitrary power.

    :param number_one: int - the base number.
    :param number_two: int - the power to raise the base number to.
    :return: int - number raised to power of second number

    Takes number_one and raises it to the power of number_two, returning the result.
    """

    return number_one ** number_two

  number_to_the_power_of_default(4) # 16
```

### Add a mutable object as a default argument

You may sometimes want to pass an **empty** [list](./7cxo.md) or
[dictionary](./0loj.md) as a default value. The problem is that **this are
mutable objects** and may not remain empty after several function call

To **solve this** you can define them as `None` and then check for it before
setting up the mutable object

```py
  def my_func(arg_1, arg_2=None):
      if arg_2 is None:
          arg_2 = []
```

### Define a function that takes any number of optinal arguments

You can use the [unpacking](./hsr4.md) operator `*` for [iterators](./p7q9.md)
to allow your function to take any arbitrary amount of extra parameters

The **convention** is to use `\*args` but **you can use any name** if it better
suits your function readability

```py
  shoping_list = {}

  def add_items(shopping_list, *item_names):
      for item_name in item_names:
          shopping_list[item_name] = 1

      return shopping_list

  shopping_list = add_items(shopping_list, "Coffee", "Tea", "Cake", "Bread")
```

### Define a function that takes any number of keyword arguments

You can define an arbitrary number of keword arguments that can be passed to
you function with the **unpacking operator** \*\* this will indicate that the
unpacking should be done into a dictionary

```py
  shopping_list = {}

  def add_items(shopping_list, **things_to_buy):
      for item_name, quantity in things_to_buy.items():
          shopping_list[item_name] = quantity

      return shopping_list

  shopping_list = add_items(shopping_list, coffee=1, tea=2, cake=1, bread=3)
```

### Unpack multiple arguments in a function call

In case that you are lazy to write all the arguments inside the function call
or you just want to **have it separete in a list or dictionary** object you can do
**multiple unpackings** inside a function call

```py
  def add(*args):
      return sum(args)

  a = [1, 2, 3]
  t = (4, 5, 6)

  result = add(*a, *t)
  print(result)             # 21
```

### Define keyword only parameters

If you want to have parameters that can only be passed by explicitly
referencing them by their keyword you can use a bare `\*` between your
positional parameteres and your keyowrd parameters

```py
  def oper(x, y, *, op):
      if op == '+':
              return x + y
      elif op == '-':
              return x - y
      else:
        return None

  oper(3, 4, '+')   # TypeError: oper() takes 2 positional arguments but 3 were given
  print(oper(3, 4, op='+'))     # 7
```

### Define positional only argumets

This are arguments that can only be referenced positionally and they can't be
referecend by their keyword. You denotate them by the `/` argument, so any
parameter by the left of it is a positional only parameter

In this example:

- x and y are positional-only
- a and b are keyword-only
- z and w may be specified positionally or by keyword

```py
  def f(x, y, /, z, w, *, a, b):
      print(x, y, z, w, a, b)
```
