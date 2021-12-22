# lang.py.oper.function.lambda

Anonymous, single use or just throw away functions

## Synopsis

```py
  assigened_function = lambda <args>: <returned-value>
```

## Overview

Anonymous functions that are most commonly used on arguments to other
[functions](./8xrz.md). Thou they can be pass to a variable to be referenced later

## Cookbook

### Pass lambda to a variable for later reference

You can pass your lambda function to a variable and called with that variable name

```py
  add5 = lambda x: x + 5
  print(add5(10))           # 15
```

### Pass a lambda function as a key argument

Some built-in functions like `min()`, `max()` and [sorted()](./8ykp.md) let you
pass a `key=<func>` argument where it will **perform** it's operation **based
on** the **results** that the passed **function gives for each** of the
arguments

```py
  numbers = [-3, -2, 4, 5]
  min_numb = min(numbers, key=lambda x: x % 2)      # -2
```
