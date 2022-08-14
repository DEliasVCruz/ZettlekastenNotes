# lang.py.module.zip.zipfile

Built-in module to maniputlate zip files

## Synopsis

```py
  from zipfile import ZipFile
```

## Overview

This is the built-in and pure python module for manipulating zip files
it works similar to the basic [file manipulation](./7i8g.md) operators by exposing
the `ZipFile` object

## Cookbook

### Print the contents of a zipfile

You can use the `ZipFile` object to manipulate a zip file within a [context
manager](./1rwn.md). The default mode is `r` for reading from a zip file

- You can use the `printdir()` method to print the contents of zipfile to
  stdout
- It can accept [path like](./bwao.md) objects

```py
  from zipfile import ZipFile

  with ZipFile("sample.zip", mode="r") as archive:
      archive.printdir()

# StdOut
File Name              Modified             Size
hello.txt       2021-09-07 19:50:10           83
lorem.md        2021-09-07 19:50:10         2609
realpython.md   2021-09-07 19:50:10          428
```

### Check if you are opening a valid zipfile

You can check if you are opening a valid zip file by either:

- Catching the `BadZipFile` [error](./t7gf.md) thrown when you try to open an
  invalid zipfile with a [try/catch](./wvgx.md) block

```py
  from zipfile import ZipFile, BadZipFile

  try:
      with ZipFile("bad_sample.zip") as archive:
          archive.printdir()
  except BadZipFile as error:
      print(error)

# File is not a zip file
```

- Using the `is_zipfile()` function to check if a file is a valid
  zipfile

```py
  from zipfile import ZipFile, is_zipfile

  if is_zipfile("bad_sample.zip"):
      with ZipFile("bad_sample.zip", "r") as archive:
          archive.printdir()
  else:
      print("File is not a zip file")

# File is not a zip file
```

### Write into a zipfile

You can write into a zipfile with the `ZipFile` object by using the `w` or `a`
mode for writing or appending to a zip file respectively

This use an existing zipfile or create a new one if it doesnt exist,
even if you don't do anythign it will still create an empty zipfile.

- It will not create new directories if they don't exit, it will throw a
  `FileNotFoundError` error

The `w` option will overwrite any existing zipfile, you can use the `x` mode
to exclusively create new ZIP files and write new member files into them.

- This is usefull if you don't want to overwrite existing ones

```py
  from zipfile import ZipFile

# This creates a hello.zip file containing hello.txt file

  with ZipFile("hello.zip", mode="w") as archive:
      archive.write("hello.txt")

# This adds a new_hello.txt file to the hello.zip file
# Creates a new one if it doesn't exist

  with ZipFile("hello.zip", mode="a") as archive:
      archive.write("new_hello.txt")
```

### Get info on the files in a zipfile

You can info from either:

- A single file from the zipfile with `.getinfo(<filename>)`
- A list of `ZipInfo` objects to [iterate](./p7q9.md) over with `.infolist()`

This returns a `ZipInfo` object or al [list](./7cxo.md) of `ZipInfo` objects
and has the following attributes

- `.file_size`: The original file size of the file
- `.compress_size`: The file of the file after compression
- `.filename`: The name of the file
- `.date_time`: A [tuple](./hsr4.md) of the [datetime](./xu7z.md) argument parts

```py
  from zipfile import ZipFile
  from datetime import datetime

  with ZipFile("sample.zip", mode="r") as archive:
      info = archive.getinfo("hello.txt")

  info.file_size    # 83
  info.file_name    # 'hello.txt'
  info.date_time    # (2021, 9, 7, 19, 50, 10)

  with zipfile.ZipFile("sample.zip", mode="r") as archive:
      for info in archive.infolist():
          print(info.filename)
          print(datetime(*info.date_time))
```

### Iterate over the files in a zipfile

You can iterate over the names of the files in a zipfile with
the `.namelist()` method. It will return a valid name argument
for `.geingo()` method for each file in your zipfile

```py
  from zipfile import ZipFile

  with ZipFile("sample.zip", mode="r") as archive:
      for filename in archive.namelist():
          print(filename)

# Output
# hello.txt
# lorem.md
# realpython.md
```

### Extract files from a zipfile

You can extract either:

- Individual files with the `.extract()` method
- All the member files with the `.extractall()` method

Both will overwrite files if they already exist and take a
destination `path=` which will be created automatically if it
doesnt exist and by default it will be the `cwd`

```py
  from zipfile import ZipFile

  with ZipFile("sample.zip", mode="r") as archive:
      for file in archive.namelist():
          if file.endswith(".md"):
              archive.extract(file, path="output_dir/")

# Output
# 'output_dir/lorem.md'
# 'output_dir/realpython.md'
```
