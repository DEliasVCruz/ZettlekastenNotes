# cli.wc

Count the number of lines, words or characters

## Synopsis

```sh
  wc [options] [files]
```

## Overview

**Print newline, word for each FILE**, and a total line if more than one FILE is
specified.

## Options

- `-l`: Print the **lines** count
- `-w`: Print the **word** count
- `-m`: Print the **character** count (including special characters)
- `-c`: Print the byte counts

## Cookbook

### Print the line count in a file

```sh
  cat myfile.txt | wc -l
```

### Print the character length of string

```sh
  echo "Hello" | wc -m
  ... 5
```

### Print the number of bites of a file

```sh
  wc -c my_file
  ... 19366 my_file
```
