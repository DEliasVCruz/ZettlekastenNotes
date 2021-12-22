# lang.py.type.number

Python has three different number types: integers (int), floating-point
(float), and complex (complex)

## Overview

You **can turn** any of this **number type** into **another** one of their
**sub-category** or a **different type** (int, float, complex)

### Integers

Whole numbers such as **hexadecimal** (`hex()` prefixed by `0x`), **octals**
(`oct()` prefixed by `0o`), and **binary** (`bin()` prefixed by `0b`) without

With their [constructor](./61fj.md) methods you can **convert from one**
display **to another**

### Floats

Numbers **containing a decimal point**

### Complex

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

### How to round a float into an int

You can round a **decimal number** (`float`) into a **round number** (`int`)
with the built-in function `round()`

By defualt it rounds to the **nearest int** based on **one decimal point**

```py
  score = 75.49
  score2 = 75.51
  rounded_score = round(score)      # 75
  rounded_score2 = round(score2)    # 76
```

- [How to Round Numbers in Python](https://realpython.com/python-rounding/)

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
