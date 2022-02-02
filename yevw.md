# lang.py.debug.pdb

The standard library module for Python debugging

## Synopsis

```py
  breakpoint()
```

## Overview

You can create breakpoints and stop your programs execution at any point to
inspect it's elements with the [pdb cli](./i158.md) interface

## Cookbook

### Create a break point in your code

Setting a `breakpoint()` in your code will stop execution of your code and
prompt you to engage wit the interactive debugger and enter commands

```py
  lis = [1, 2, 3]
  lis.append(4)

  breakpoint()

  lis.pop()
```
