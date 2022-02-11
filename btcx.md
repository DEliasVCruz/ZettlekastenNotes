# cli.sort

Sort lines of text in a file

## Synopsis

```bash
  sort [options] [file]
```

## Overview

Sort can take **stdin** but it can only sort **new line separated** strings

## Options

- `-u`: Sort and leave only unique values
- `-r`: Sort on reverse order
- `-n`: Sort numerically
- `-R`: Do a random sort
- `--ignore-case`: Sort ignoring casing

## Cookbook

### Sort and get unique lines

You can use the `-u` option to get **only the unique values** after sorting. For
**more options** for working with unique values check [uniq](./kxv.md)

```sh
  sort -u file.txt
```

### Sort based on numerical values

By **default** it will sort based on the `ASCII` table (alphabetic order), if
you want **to sort numbers** you need to **pass** the `-n` option

```sh
  echo "4\n3\n2" | sort -n
  -> 2
  -> 3
  -> 4
```

### Sort a string of space separated characters

If you have a string of **substrings** separated but some **delimiter other
than** `\n`, you can first pipe the string through [tr](./bjmz.md) and then
pipe it into `sort`

```bash
  words_to_sort="fruit apple game day"
  sorted="$(echo "${words_to_sort}" | tr " " "\n" | sort -u | tr "\n" " ")"
```

### Sort the characters of a single word string

If you want to sort the characters in a string. First you have to **split
them** by a delimiter, you can do this by **appending them to** an
[array](./800e.md) in bash

```bash
  # Turn it into an array
  letters_array=()
  for ((i = 0; i < ${#letters}; i++)); do
    letters_array+=("${letters:i:1}")
  done

  # Sort the string
  sorted="$(echo "${letters_array[*]}" | tr " " "\n" | sort -u | tr "\n" " ")"
  sorted="${sorted// /}"
```
