# lang.bash.type.command

Bash understands five types of commands: aliases, functions, builtins,
keywords, and executables.

## Overview

## Aliases

Is a way of **shortening a command**, and they are **only used in** an
**interactive** shell and **not in scripts**

```sh
  alias nmapp="nmap -Pn -A --osscan-limit"
```

They are **limited in power**, the replacement only happens in the first word.
For **more flexibility**, use a **function**

## Functions

A [function](./d1jy.md) is **like aliases** but **more powerful**. It contains shell
commands, and is **similar to a small script**

## Builtins

The **basic commands** that are built into it like `cd`

## Keywords

They allow you to interact with bash in different ways by **modifying** it's
**behaviour**. They can come in the form of [special characters](./tmd3.md)

For example the **keyword** `[[ ]]` for **extended test** that is different
from the `[ ]` builtin.

Under **the later** a character like `<` will mean [redirection]() but in **the
former** it will act as the **normal comparison operator**

```sh
  [ a < b ]
  -bash: b: No such file or directory
  [[ a < b ]]
```

## Executables

This are **external commands** that are known to `Bash` through the `PATH`
variable, which is a set of **directory names separated by colons** 
