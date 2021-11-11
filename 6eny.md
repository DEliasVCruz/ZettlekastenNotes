# lang.bash.type.arguments

In bash arguments and commands need to be separated by spaces

## Overview

We want the `command` to be separated by **whitespaces**. For example, the
**following** would be **wrong**:

```sh
  [-f file]
```

In this case `bash` will think that you are trying to execute a command named
`[-f` with the argument `file]`.

The **correct command** separates all arguments with whitespaces:

```sh
  [ -f <file> ]
```

If your **argument contain white spaces** or [special characters](./tmd3.md)
they need to be **surrounded** by **quotes** such as `"file name with spaces"`

## Cookbook

### Store arguments for later use

You can use a [variable](./y2lh.md) as an [array](./800e.md) to store arguments to
pass to a [command](./rffs.md)

```sh
  args=(-s "$subject" --flag "arg with spaces")
  mail "${args[@]}"
```
