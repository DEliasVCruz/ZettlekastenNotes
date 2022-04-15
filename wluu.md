# cli.read

Read from stdin to shell variables

## Synopsis

```sh
  <pipe-operations> | read <variable>
```

## Overview

You can use the `read` command to asing output of commands through `piping` it
by `stdin`

## Cookbook

### Asign the output of a command into a variable

You can capture the output of command and **pipe it** into a variable and then
reference it by normal shell [variable expansion](./wluu.md)

```sh
  echo "Hello World" | read h
  echo "$h"
# > Hellow World
```
