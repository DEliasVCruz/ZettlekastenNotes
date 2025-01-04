---
tags: ["linux", "system", "storage", "comandline"]
---

# cli.du

Estimate and summarize file and directory space usage

## Synopsis

```sh
du [<options>] <file[s]|path>
```

## Overview

The comand name is short for `disk usage`

### Options

- `-s`: Display only the total size for each file or directory
- `-h`: Print the sizes in human readable format (1K 234M 2G)

## Cookbook

### Get the size of a directory

You can use the `-s` and `-h` flags to show the size of a
single directory, in human readable units

```sh
du -sh <path/to/directory>
# 160M  <path/to/directory>
```
