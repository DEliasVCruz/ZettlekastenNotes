# lang.py.type.error

Python has an extensive list of built in errors for different circumstances

## Overview

For the most part you should **limit yourself to use** the builtin errors that
python defines

## Cookbook

### Raise a custom error message

You can raise an error with the `raise` keyword. Furthermore you can **specify
a custom** error message

```py
  if [condition]:
    raise ValueError("Wrong Value Inputed!")
```

### File related errors

- `FileNotFoundError`: when a file or directory is requested but doesn’t exist.
- `OSError`: In a system function related error (see [os](./ik75.md) module)
- `BadZipfile`: custom error for invalid zipfiles from the [zipfile](./9lfj.md) module

### Operations related errors

- `RecursioError`: When the maximum depth of a recursion function has been reached

### General error

- `IndexError`: When trying to reach and index outside of reach, in a sequence

### Indexing related error

- `KeyError`: When you try to access an index that is out of range or does not exists
