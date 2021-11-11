# cli.xargs

It takes output of a command and passes it as argument of another command

## Overview

It let's you build and execute commnand lines form standard input, it is
**helpfull** for **use** with other **tools that can't accept standard input**
as a parameter.

It reades **items** from standard input as **separated by blanks** and
**executes** a **command on each argument**.

It is mostly used to operate on the output of another command like `find`

**Blank lines** on the standard input **are ignored**

## Synopsis

```h
  stdin | xargs [options] [command [arguments ..]]
```

## Options

- -d: Change delimeter for standard input arguments
- -t: Prints each command that will be executed to the terminal
- -p: Prompt for confirmation before executing the resulting command
- -I: Replace defined placeholder with the passed arguments

## Cookbook

### Run multiple commands at once

You can run multimple different commands at once using the **same argument list**
from stdin by defining a **placeholder** that will be **replaced** on the
**commands skeleton**

In this example the **placeholder** `%` is **defined** and will be **replaced**
with the arguments **"one two three"**

```sh
  echo "one two three" | xargs -I % sh -c 'echo %; mkdir %'
```

### Deal with file names with blank spaces and newline

**Sometimes** the stdin arugments may contain **blank spaces or newlines** that
**will break the structered command**. For this cases the `-O` option wil take
care of this.

```sh
  find . -iname "*.mp3" -print0 | xargs -0 -I % mplayer %
```

### Convert multi-line output into sinle line

You can turn a multi-line output, like the one `ls` gives, into a single space
separated line

```sh
  ls /path/to/dir/ | xargs
```

### Display the number of lines/words/characters in a list of files

You can pair with `ls` and `wc` for when you want to know how many **words, lines
or character for each file**.

```sh
  ls /path/to/dir/ | xargs wc
```
