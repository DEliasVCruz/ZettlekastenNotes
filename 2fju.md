# lang.py.module.tempfile

Built-in module to create temporary files and directories

## Synopsis

```py
  from tempfile import TemporaryFile, TemporaryDirectory
```

## Overview

## Cookbook

You can use it to create files and directories that will
be deleted once the created resource is closed

### Create a temporary directory

You can create a new temporary directory in your systems
default temporary objects path by using the `TemporaryDirectory`
class

- You can get the path name of the created directory as a [string](./4t3v.md)
  with the `.name` attribute
- You can manually delete the created temp directory using the `.cleanup()`
  method

You can use it in a [context manager](./1rwn.md) and it will handle clean up
automatically. It will pas the contents of the `.name` attribute

```py
  from tempfile import TemporaryDirectory

  with TemporaryDirectory() as tmpdirname:
      print(f"Created temporary directory {tmpdirname}")

# Created temporary directory /tmp/tvwdfuwlfh
```
