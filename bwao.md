# lang.py.module.pathlib

Manipulate paths and the underlying file system

## Synopsis

```py
  import pathlib

  path = pathlib.Path.<from>()
```

## Overview

With this you can read and write [files](./7i8g.md), **manipulate paths and** the
underlying **file system**, as well as **list files** and **iterate over them**

The basics **consist of** the `pathlib.Path` [class](./unhs.md) which is **not
a string** so it **does not inherit** the same methods and properties **from**
[strings](./4t3v.md)

## Cookbook

### Create a Path object

There are multiple ways to create a path object:

- `cwd()`: Create a path object from the current working directory
- `home()`: Create a path object from the home directory

You can also crete a path object **from it's string representation** or by
appending a combination of paths objects and strings with `/` or the
`joinpath()` method

```py
  pathlib.Path.cwd()                                       # Current working directory
  pathlib.Path.home() / 'Descargas'                        # ~/Descargas
  pathlib.Path.home().joinpath('Descargas', 'preuba.txt')  # ~/Descargas/prueba.txt
  pathlib.Path(r'~/Descargas/prueba.txt')                  # ~/Descargas/prueba.txt
  pathlib.Path('test.md')                                  # <cwd>/test.md
```

### Open a file

You can open a file **with** the traditional `open()` **function** since it
accepts a `Path` object. **Or** you can **use** the `Path.open()` method

```py
  path = pathlib.Path.home().joinpath('Descargas', 'prueba.txt')
  with path.open(mode='r') as file:
    ...
```

There are also some **methods for reading and writing files**, that **handle** the
**resource manage by themselves** without the need of a [congext
manager](./1rwn.md).

- `read_text()`: **Return** the contents of the file as a [string](./4t3v.md)
- `read_bytes()`: Open in bynary mode and return the contents as a bytestring
- `write_text()`: Write string data to the file
- `write_bytes()`: Open in bynary mode and write byte data to the file

```py
  path = pathlib.Path.cwd() / 'test.md'
  print(path.read_text())                   # Print the contents as a string
```

### Find the full path to a file

You can **use** the `resolve()` method to find the full path of a `Path`
object. You **can also use** the `absolute()` method

```py
  path = pathlib.Path('test.md')
  print(path.resolve())                     # /home/danielv/test.md
  print(path.absolute())                    # /home/danielv/test.md
```

### Picking components of a path

You can **access different parts** of the `Path` object with this attributes:

- `name`: The file name without any directory
- `parent`: The directory path containing the file or directory
- `stem`: The file name without the file extesion
- `suffix`: The file extension
- `anchor`: The filepaht delimeter
- `parts`: Returns a tuple with **every element from the path**
  - **Includes root directory**
  - **Excludes delimeters**
- `parents`: Returns a **list** of the **full paths** of **all parent directories**

```py
  print(path.name)          # prueba.txt
  print(path.stem)          # prueba
  print(path.suffix)        # .txt
  print(path.parent)        # /home/danielv/Descargas
  print(path.parent.parent) # /home/danielv
  print(path.anchor)        # /
  print(path.parts)         # ('/', 'home', 'danielv', 'Descargas', 'prueba.txt')
```

**Every attribute** aside from `parent` **_returns strings_** and they can be
used as such. The `parent` attribute **returns a new** `Path` object

```py
  path.parent.parent / ('new' + path.suffix)    # /home/danielv/new.txt
```

### Check if a path exists

You can **check** if a directory **path or file exists** with `exists()`
returns a [boolean](./6auy.md) object

```py
  path = pathlib.Path('file.txt')
  print(path.exists())              # False
```

### Check if a path is a file or a directory

You can **use** `is_dir` and `is_file` **methods** to find if a path is a file
or a directory. They **return** a **boolean**

```py
  path.is_dir()         # False
  path.is_file()        # True
```

### Moving and deleting files

You can perform basic file system level operations like moving, updating and
deleting files. They do this without given warnings

- `replace()`: **Move** a **file** to a new location.
  - If the destination already exists it will overwrite it

To **write a file and ensure it does not exist** yet you can structure like

```py

source = pathlib.Path('old/path/file.txt')
destination = pathlib.Path('new/path/file.txt')

if not destination.exists():
    source.replace(destination)
```

### Iterate over the files in a direcotry

You can **use** the `iterdir()` method to **iterate** over **all files** in the
given directory by **return** an [iterable](./p7q9.md) object

You can use it, as in this example, to count files by file extension. Here we
leverage the `Counter` object from the [collections]() libarary

```py
  import collections

  collections.Counter(p.suffix for p in pathlib.Path.cwd().iterdir())
  # Counter({'.md': 2, '.txt': 4, '.pdf': 2, '.py': 1})
```

### Get information about a file

You can **use** the `stat()` **method** to get information about a file such as:

- `st_mtime`: Time of last modification of a file
- `st_ctime`: Time of creation of a file
- `st_size`: Size of a file

The `st_` **time** properties **represent seconds since January 1st, 1970**. And
can be **converted to** more usefull **time formats** with the [datetime]() or
[time]() module.

```py
  from datetime import datetime

  time, file_path = max((f.stat().st_mtime, f) for f in directory.iterdir())
  print(datetime.fromtimestamp(time), file_path)
  # 2018-03-23 19:23:56.977817 /home/gahjelle/realpython/test001.txt
```

### Find files with a glob patter

You can return an **iterable** (**list**) of all the files in a given direcotry
that match a **glob** patter with:

- `glob()`: Find files based on a glob pattern (`*`, `?`) in the **current directory**
- `rglob()`: Find files based on a glob pattern **recursively on all directories**

```py
  import collections

  collections.Counter(p.suffix for p in pathlib.Path.cwd().glob('*.p*'))
  # Counter({'.pdf': 2, '.py': 1})
```

### Find a path relative to another path

If you want **display** a path **as a relative path to another path** you can
use the `relative_to()` method

In this example we use it to **create a directory tree**

```py
  def tree(directory):
      print(f'+ {directory}')
      for path in sorted(directory.rglob('*')):
          depth = len(path.relative_to(directory).parts)
          spacer = '    ' * depth
          print(f'{spacer}+ {path.name}')
```

### Rename a file

You can perform **file renaming** with the `rename()` method

```py
  path.rename('new_name.txt')
```

### Create a direcotry from a path

You can use the `mkdir()` method to create a directory from a `Path` object

```py
  path = pathlib.Path.cwd() / "new_dir"
```
