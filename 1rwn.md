# lang.py.oper.context_manager

Ensure the correct management of resources handling access and closing

## Synopsis

```py
  with <accessed-resourced> as <alias>:
      <operation-block>
```

## Overview

When you have a **resource** or functionality that **has preconditions** and
**post-conditions** that **need to be met** when you use this resource or
execute this functionality

**Like** accessing a database or **opening a file**, to whom the **connection**
has to be **closed after** to avoid resource leaks and to free it up for later
use

There are **two ways** to **create** your own context manager:

- A custom [class](./unhs.md)
- Using a [generator](./grh0.md) function with [contextlib]() module
- Using [functions](./8xrz.md) and [decorators](./ff01.md)

## Cookbook

### Create a context manager with a custom class

To create a custom context manager with a class all you need to do is **specify**
in your class the [magic methods](./a8n3.md):

- `__enter__`: It will be **executed** when the `with` block is **initialized**
- `__exit__`: It will be **executed** after the `with` block is **exited**

```py
  class FileHandler():

      def __init__(self, file_name, file_mode):
          self._file_name = file_name
          self._file_mode = file_mode

      def __enter__(self):
          self._file = open(self._file_name, self._file_mode)
          return self._file


      def __exit__(self, exc_type,exc_value, exc_traceback):
          self._file.close()

  if __name__ == "__main__":

      with FileHandler('test.txt', 'w') as f:
          f.write('Test')
```

### Create a context manager using a generator

You can create a context manager with a **generator function** alongside the
`@contextlib.contextmanager` decorator from the `contextlib` module

Here **everything before** the `yield` [statement](./4g9v.md) will be treated
as if it where **part of** the `__enter__` method and **everything after** it
will be **treated as** part of the `__exit__` method

```py
  import contextlib

  @contextlib.contextmanager
  def file_hanlder(file_name,file_mode):
      file = open(file_name,file_mode)
      yield file
      file.close()

  if __name__ == "__main__":

     with file_hanlder("test.txt","w") as f:
         f.write("Test")

     print(f.closed)
```

### Create a context manager using a function decorator

You can use a custom decorator but is conversome and it's not possible to
access the value returned by the `__enter__` method. Thus **is not
recommended**
