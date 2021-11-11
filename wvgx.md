# lang.py.oper.exception

A control flow for error handling

## Synopsis

```py
  try:
    <operations>
  execpt <exception_name> as <alias>:
    <operations_if_try_raises_exception>
  else:
    <operations_if_try_succeds>
  finally:
    <operations_that_always_execute>
```

## Overview

You can handdle [errors](./t7gf.md) with this operation flow. Keep in mind that this
serves so **the raised exception won't be exposed** to the user and it **will
not stop the program** from continue executing.
