# cli.seq

Print a sequence of numbers on the comandline

## Synopsis

```sh
seq [options] [first] [increment] <last>
```

## Overview

Print numbers from `first` to `last` in steps of `increment`, if `first`
or `increment` is omitted they default to `1` respectively

### Options

- `-f`: use printf style formatting for the output
- `-s`: use a custom separator for each number (default is `\n`)
- `-w`: equilize width by padding with leading zeros

## Cookbook

### Print a list of number separated by space

You can use the `-s` flag to provide a custom separator

```sh
seq -s " " 4
# 1 2 3 4
```

### Print a list of formatted strings with numbers

You can use the `-f` flag to format the way that the
numbers are printed, thus allowing you to specify a custom
string to print for each value

```sh
seq -s ", " -f "Message number %g" 1 3
# Message number 1, Message number 2, Message number 3
```
