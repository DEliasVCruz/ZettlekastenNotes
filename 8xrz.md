# lang.py.syntax.function

Your standard function definition but in Python

## Synopsis

```py
  def function_name(args):
    # Operations
    [return|yield]
```

## Overview

Functions that **do not have an explicit** `return` [statement](./4g9v.md) **will
return** [None](./y624.md)

- You can create functions with none, any or default [arguments](./1zjl.md)
- You can also create anonimous functions with [lambda](./8uan.md) expressions

## Statements

- `return`: Explicitly return a value or object and exit function
- `yield`: Returns a [generator](./grh0.md) object

### The yield statement

Unlike `return` this **will not exit** out of your **function**. You can still
do operations after it

Here **after each yield** the **state** of the function **is remembered** on
the next call

Using it in a fucntion **will create** a [generator](./grh0.md) object

## Cookbook

### Create a docstring for documentation

It is **recommended** that every function **includes a docstring** since they
can **help on building documentation** and are return by calling `.__doc__()`
**on the function, method or class name**

The structure of a **docstring** is as follow:

```py
  """Short one line summary

  :param <param_name>: <type> <short_description>
  # Repeat for every defined argument
  :return: <type> - <description_of_the_returned_value>
  """
```

### Use a conditional statement inside a return expression

You can write a **conditional statment inside a return expression** as a one liner

```py
  def min(a, b):
      return a if a < b else b
```
