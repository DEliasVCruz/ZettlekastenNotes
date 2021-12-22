# lang.py.type.hints

Type annotations for your variables, arguments and function results

## Synopsis

```py
  arg: <type> = <value>

  def my_func(arg: <type> [= <default>]) -> <return-type>:
      pass
```

## Overview

You can **annotate**  with **type hints** that **can serve as documentation** or
reminders of what are their expected value type

However, **they are not enforced** by the interpreted **as strog typing**, they only
serve as hints

You can annotate:

- Variables
- Arguments
- [Functions](./8xrz.md)

## Cookbook

### Type hint a variable

```py
  decimal_number: float = 13.4
```

### Type hint a function arguments and it's result

```py
  multiply_by(number: int, multiple: int = 2) -> int:
      return number * multiple
```
