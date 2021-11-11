# cli.sort

Sort lines of text in a file

## Synopsis

```bash
  sort [options] [file]
```

## Overview

Sort can take **stdin** but it can only sort **new line separated** strings

## Options

- -u: Sort and leave only unique values

## Cookbook

### Sort a string of characters

If you have a string of **substrings** separated but some **delimeter other
than** `\n`, you can first pipe the string trhoug [tr]() and then pipe it into
`sort`

```bash
  words_to_sort="fruit apple game day"
  sorted="$(echo "${words_to_sort}" | tr " " "\n" | sort -u | tr "\n" " ")"
```

### Sort the characters of a single string

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
