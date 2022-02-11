# cli.ripgrep

The advance grep command written in rust

## Synopsis

```sh
  rg [options] <pattern> [directorie[s]|file[s]]
```

## Overview

You can use `rg` as a simplified and faster `grep` command to filter text and
lines from files with regular expressions.

It respects [git](./i0ps.md) repos by default and it does not search through
files and directories specified in a `.gitignore` file

- Other **default options** are:

  - Doesn't search through hidden files (dot files)
  - Recursively searches pattern in current directory
  - Colored output
  - Uses the full [regex syntax](./cbw4.md)

### Options

- `-t`: Search only on specified file types
- `-uu`: **Search** through **all files**
- `-g`: Search through **files that match a glob**
- `--files-with-matches`: Only output the file names of the matches
- `--invert-match`: Output lines that don't match the pattern
- `-F`: Search a literal string (**no regex pattern**)

## Cookbook

### Search only inside specified file types

You can set it to only search inside **specify file types** with the `-t` option

```sh
  rg -t python 'my_func'
```

You can also **achieve something similar** with the `-g` option to specify **glob
files** to search on

```sh
  rg 'my_func' -g '*.py'
```

### Search through all the files

By **default** `rg` will **not search through** files specified at `.gitignore`
files nor hidden (**dot files**)

You can use the `-uu` option to **search through all files** including hidden
and `.gitignore` files

```sh
  rg -uu 'my_func'
```

### Search through a set of subdirectories

By **default** `rg` will **search recursively** through **all** the
**directories of** the current **working directory** where it's called

You can **specify** only a set of **directories** you want **to search through**

```sh
  rg 'my_func' path/to/directory path/to/other/directory
```

### Only get the file names of the matches

By default `rg` will output the lines where the match was found for each file.
You can use the `--files-with-matches` to get only the file names where a match
was found

```sh
  rg --files-with-matches 'my_func'
```

### Use along the `ps` command

When you use it along the `ps` command it will return also the `rg` process to
avoid this sourround the first letter of your pattern with `[]`

```sh
  ps aux | rg '[s]t$'
```
