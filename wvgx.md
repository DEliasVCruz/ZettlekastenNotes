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

You can handle [errors](./t7gf.md) with this operation flow. Keep in mind that this
serves so **the raised exception won't be exposed** to the user and it **will
not stop the program** from continue executing.

You’ll want to refer to specific exception classes you want to catch and
handle. So be specific about what error you are expecting

### Cookbook

### Chain exceptions

You can **chain two exceptions** together with the `from` clause, that will **attach**
the exception **as the caused** of the **manually raised exception**

```py
  try:
    print(1 / 0)
  except Exception as e:
    raise RuntimeErro("Something bad happened") from e
```

You can **explicitly suppressed the exception chaining** (the cause exception)
by passing `None` to the `from` clause

```py
  try:
    print(1 / 0)
  except Exception:
    raise RuntimeErro("Something bad happened") from None
```

### Define multiple exceptions to catch

You can define a variety of `exception` blocks inside your `try` block and will stop
at the first exception that it hits

In this way you can **anticipate multiple exceptions** and differentiate how the
program should respond to them.

```py
  try:
      linux_interaction()
      with open('file.log') as file:
          read_data = file.read()
  except FileNotFoundError as fnf_error:
      print(fnf_error)
  except AssertionError as error:
      print(error)
      print('Linux linux_interaction() function was not executed')
```

### Define a exception message and traceback

You can define a **custom error message** for your raised exception and a
custom **traceback object** with the `with_traceback()` method

```py
  raise Exception("foo occurred").with_traceback(tracebackobj)
```
