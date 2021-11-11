# lang.bash.type.exit_status

Every command results in an exit code whenever it terminates. They function as
**thruthys and falsies** for conditional expressions

## Overview

Is used by a programm to **evaluate if everything went OK**. It also functions
as a **booleanish type**.

An exit code can be **any integer between 0 and 255**, where **0 is a truthy**
and indicates **success** and **any other number is a falsy** to indicate
**failure** of some sort

## Commands

- `!`: Negate the exit statement

## Cookbook

### Use exit code as variable

The [special parameter](./y2lh.md) `?` displays the **exit code** of the last
terminated foreground process

```bash
  if [[ $? -eq 0 ]]; then
    <operation-on-succes>
  elif [[ $? -eq 1 ]]; then
    <operation-on-failure>
  fi
```

### Return a failure non-zero exit code

To return a **non-zero** exit code when somethin unexpected happens and your
**script failts to run correctly**

You can do this **with the** `exit` builtin. Keep in midn that **the srcipt or
function will stop** uppon encountering the `exit` command

```bash
  if [[ condition ]]; then
    <operation-on-succes>
  else
    exit 1;
  fi
```

### Negate a command exit status

**Similar** to what you would specify as `not` **in other programming
languages** you would use the `!` command to **tunr a succes (0) into a
failure** and **viceversa**

```bash
  if ! [[ condition ]]; then
    <operation-on-reverse-condition>
  fi
```

### Output a custom error message

Is very straightforward, just `echo` your **error message before** your `exit`
code

```bash
  if [[ "${#@}" -eq 1 ]]; then
    echo "Hello, $1"
  else
    echo "Usage: error_handling.sh <person>"
    exit 1
  fi
```
