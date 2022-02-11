# cli.uniq

Show all the lines without duplication

## Synopsis

```sh
  sort <file> | uniq [options]
```

## Overview

It's use in conjuction with [sort](./bcx.md) analize unique and not unique
lines in a file or `\n` separated string

Some of the options are:

- `-c`: Count **how many times** each **line is repeated**
- `-d`: **Get** only the **lines** that **had duplicates**
- `-u`: **Get** only the **lines** that **had no duplicates**
- `-dc`: Get only **duplicate** lines and display **how many times each was repeated**

## Cookbook

### Get all the unique lines

You are better off using the `sort` option of `-u`

```sh
  sort -u file.txt
```

### Get only the lines that had duplicates

You can display only the **lines** that had **more than one repetition** with
the `-d` option

```sh
  echo "hello\nworld\nhello" | sort | uniq -d
  -> hello
```

### Get the number of repeated lines

You can **get** the **list of repeated lines** along side their **repetition
count** with `-dc` options

```sh
  echo "hello\nworld\nhello" | sort | uniq -dc
  -> 2 hello
```

### Get only the lines that had no duplicates

You can use the `-u` option to only return the **lines that where already
unique**

```sh
  echo "hello\nworld\nhello" | sort | uniq -u
  -> world
```

### Get the number of not repeated lines

If you use the `-u` You will **get only the lines that had no duplicates** you
can **pair it with** [wc](./pcsj.md) to count how many lines had no duplicates

```sh
  echo "hello\nworld\nhello" | sort | unique -u | wc -l
  -> 1
```

### Get lines with ocurrence sorted by frequency

You can **display number of occurrences** of each line, **sorted** by the
**most frequent**

```sh
  sort file | uniq -c | sort -nr
```
