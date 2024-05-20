# lang.py.data.number

Python has three different number types: integers (int), floating-point
(float), and complex (complex)

## Overview

You **can turn** any of this **number type** into **another** one of their
**sub-category** or a **different type** (int, float, complex)

- **INTEGERS**:

  Whole numbers such as **hexadecimal** (`hex()` prefixed by `0x`), **octals**
  (`oct()` prefixed by `0o`), and **binary** (`bin()` prefixed by `0b`) without

  With their [constructor](./61fj.md) methods you can **convert from one**
  display **to another**

- **FLOATS**:

  Numbers **containing a decimal point**

- **COMPLEX**:

  By **appending** `j` or `J` to a number it **creates** an **imaginary number**.
  Then add an `int` or a `float` to create a `complex` number with **both real
  and imaginary parts**

### Arithmetics

PyPython considers **ints narrower than floats**, **which are** considered **narrower
than complex** numbers.

When numbers of **different widths** are operated together the **result** will take
the **width of the less narrow number**

So when **adding** an `int` and a `float` the result will be a float

## Cookbook

### Format a number

You can **specify formatting options** for you number inside an [f string](./4t3v.md) by
applying them after the `:` modifier

- `,`: Separate thousands with a ','
- `.<number>`: The number of floating points precision
- `f`: The number of fixed decimals to display
- `%`: display the number as a percentage

```py
  number_1 = 1000.237
  number_2 = 235.2
  floating = 0.23428
  my_string = f'The first number is {number_1:,.2f}, the second is {number_2:.2f}
  float_string = f'A percentage with two decimals {floating:.2%}'

  print(my_string)      # The first number is 1,000.24, the second is 235.20
  print(float_string)   # A percentage with two decimals 23.43%
```

### Turn a number into it's corresponding ascii character

If you want to turn a **number into the character** that it represents in the
**alphabet** you can use the built-in function `chr()`

This function will **turn it into** it's **unicode character**, so if you want
to turn it **base on the alphabet** index you will have to **add** `96` (based
on American alphabet)

```py
  character = chr(2 + 96)
  print(character)          # b
```

You can also do the same process backwards with a [string](./4t3v.md) character
with `ord()`

### Check if a number is integral

An **integral number** is a number that has **no floating point** or it's equal
to 0. With the `is_int()` method, you can use this to **check if floating
numbers don't have floating points**

```py
  number = 12.0
  number_2 = 12.002

  print(bool(number.is_int))        # True
  print(bool(number_2.is_int))      # False
```
