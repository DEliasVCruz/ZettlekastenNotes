# lang.bash.syntax.functions

Basic function syntax and use cases

## Synopsis

```sh
  [function] <function-name> () {
    <operations>
    [return] [0|<error-numbers>|<other-output]
  }

  function-name arg1 arg2
```

## Overview

You can use functions in your bash code to simplify code repetition or for
readability purposes

Functions in `bash` have some of the **following characteristics**:

- Use the `return` keyword to signal [exit status](./wokn.md)
- They don't accept any named arguments
- Arguments can be passed and reference as normal [parameters](./y2lh.md)

## Cookbook

### Use positional parameters in your function

Though a `bash` function can't take named arguments, when called it can still
take parameters like a normal script

This can then be **normally accessed** inside the function **like parameter
variables**

```sh
  fucntion my_func () {
      echo "This are all the arguments: '$@'"
      echo "This is the second '$2' variable"
    }

  my_func arg1 arg2

# This are all the arguments: arg1 arg2
# This is the second arg2 variable
```

### Exit out of a function prematurely

You can use the **builtin command** `exit` to **escape out** of a function
prematurely, you can also provide an [exit status](./wokn.md)

```sh
  function my_func () {

      if [[ "$1" = "no" ]]; then
        echo "Exiting function";; exit 0
      fi

      echo "Continue function"

    }
```
