# lang.py.oper.function

Your standard function definition but in Python

## Synopsis

```py
  def function_name(args):
    # Operations
    [return|yield]
```

## Overview

Functions that **do not have an explicit** `return` [statement](./4g9v.md)  **will
return** [None](./y624.md)

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
