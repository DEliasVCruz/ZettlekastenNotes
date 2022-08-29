# lang.py.module.atexit

Built-in module to register/unregister function execution at interpreter
termination

## Synopsis

```language
  import atexit

  atexit.register(<callable-function>[, <func-arguments>])
  atexit.unregister(<callable-function>)
```

## Overview

The `atexit` module provides two function, `register` and `unregister`, that
will ensuer that a function is executed or not at normal interpreter
termination respectively

This is usefull if you want some function to be executed before the
program exits for cleaning, loging, catching needs (to name some examples)

- You can register more than one function at any time during your scripts or
  modules before exiting
- They will be executed in reverse order of which they were `register`
  - Last registered, will be the first to be executed
- In the same way, you can `unregister` any function from exit callback

Keep in mind that no registered function will be executed if the program
terminates by:
- `InputCancel` (`<C-c>`),
- Some not normal means of exiting (like `os._exit()`)
  - Exiting through `sys.exit()` will be ok
- Some fatal python interpreter error

## Cookbook

### Register functions to be called at system exit

You can registers function to be called back at system exit at any time
by passing them as a callable object to the `register()` function

If you need to pass some arguments to the callable, you can pass them
through the `register` fucntion by passing them as extra arguments

Keep in mind that they will be executed at reverse order of which they
where registered

```py
  import atexit

  def my_cleanup(name):
      print(f"Cleaning up {name}")

  atexit.register(my_cleanup, "Carlos")
  atexit.register(my_cleanup, "Pablo")
  atexit.register(my_cleanup, "Daniel")

# The result
# Cleaning up Carlos
# Cleaning up Pablo
# Cleaning up Daniel
```

### Unregister functions from being executed at system exit

You can cancell the execution of any previously register function,
even if it was not registered it will not error out and it will just
silently handle any missing function

```py
  import atexit

  def my_cleanup(name):
      print(f"Cleaning up {name}")

  def second_cleanup():
      print("Hello")

  atexit.register(my_cleanup, "Carlos")
  atexit.register(second_cleanup)
  atexit.unregister(my_cleanup)
  atexit.unregister(third_cleanup, "Pablo")

# The result
# Hello
```

### Use it as a decorator

You can also use it as a [decorator](./ff01.md), this is usefull for cleanup functions
that operate on module-level global data

- Keep in mind that this functions need to handle the case where he resources
  it is supposed to clean up were never initialized
    - Calling the exit callbacks should not produce an error

```py
  import atexit

  @atexit.register
  def all_done():
      print('all done')


  print('starting main program')

# The result
# starting main program
# all done
```

### Handling errors

When registerd functions are calledback if they raise any errors, they will be
printed to `stdout` and the final raised error will be re-raised at the very end

Since registered functions are calledback in a LIFO fashion, some may error out
as a result of a previous error, and getting only the last error might not be
the most usufull

That is why is best to handle and quietly log all exceptions in cleanup
functions, since it is messy to have a program dump errors on exit
