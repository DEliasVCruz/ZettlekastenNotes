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
