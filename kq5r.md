# lang.py.data.number.operations

Perform basic operations on number with built-in functions

## Synopsis

```py
  round(<number>, <presicion>)
  abs(<number>)
  power(<number>, <power>, <divisor>)
```

## Overview

You can use the built in functions in `Pyhton` to round, raise to the power or
get the absolute value of a number.

## Cookbook

### Round a floting number into an integer

You can round a **decimal number** (`float`) into a **round number** (`int`)
with the built-in function `round()`

By defualt it rounds to the **nearest int** based on **one decimal point**

```py
  score = 75.49
  rounded_score = round(score)      # 75
```

- [How to Round Numbers in Python](https://realpython.com/python-rounding/)

### Round a floting into specified decimals

The `round()` function accepts a second integer argument that specifies the
round precision

```py
  number = 1.235
  number = round(number, 2)         # Round to 2 floating points
  print(number)                     # 1.24
```

### Get the absolute value of a number

You can use the `abs()` function to get the absolute number of an integer or
floating number

```py
  number = -25.3
  number = abs(number)
  print(number)                     # 25.3
```

### Elevate a number to a power

Thou you can use the `**` operator for exponential operations. You could also
use the `pow()` function to get a number by the power of another

It also **accepts a third argument** where that will apply `modulus` over the
result of the exponential operation

```py
  number = 2
  power = 2
  divisor = 2
  result = pow(number, power, divisor)
  print(result)                     # 0
```
