# lang.bash.oper.loops

Conditional loops for repeated operations

## Synopsis

```bash
  loop <condition>; do
    <operations>
  done
```

## Overview

There are **two basic kinds**, the `while` loop with it's **variant** `until`.
And the `for` that can appear in **two different forms**

## Loop commands

- `while <command>`: **Repeat** so long **as** command is executed **successfully**
- `until <command>`: **Repeat** so long **as** command is executed **unsuccessfully**
- `for <variable> in <arguments>`: Repeat the loop for each argument

## Cookbook

### Do a while loop

It will execute the operations **as long as** something happen

```bash
  while [[ true ]]
  do
    echo "Infinite loop"
  done
```

### Do an until loop

It's barely used since it is similar to `while !`

```bash
  until ping -c 1 -W 1 "$host"; do
    echo "$host is still unavailable"
  done
```

### Do a simple for loop over the file system

Bash has **built in support for itrating over files** in the file system. You can
create a simple for loop that will **go over an specified directory file** with
magic methods

```sh
  for file in *.md
  do
    echo "File Name: $file\n"
    cat "$file"
```

### Define a range to loop through

If you want a **range to loop** your variable through,
`(initial-number..last-number)` where you can **define** a number to start from
and one to end at

```bash
  for i in (10..1)
  do
    echo "$1 empty cans of beer"
  done
```

This would be the same as:

```bash
  for i in 10 9 8 7 6 5 4 3 2 1; do
    echo "$1 empty cans of beer."
  done
```

### Skip to the next iteration of a loop

You can use the built-in `continue` to **skip ahead** to next iteration
**without executing the rest of the body**

This works in **both** `for` and `while` loops

```bash
  for <variable> in <words>; do
    if <condition>; then
      continue
      # Jump to next iteration
    fi
    <operations>
  done
```

### Jump out of a loop

You can use the built-in `break` to **jump out of the loop** and **continue
with the script** after it.

This works in **both** `for` and `while` loops

```bash
  while <condition>; do
    <operations>
    if <condition>; then
      break
      # Brak out of the loop
    fi
  done
  <operations>
```

### Case statement

The syntax for creating a case statement where you **check a variable** against
different values and perform some code **if it matches**.

Can be achived with the keyword `case`, each **pattern** must be **followd by**
a `)` and **at the end** of every **code block** (operation) must come a `;;`

```bash
  case <variable> in
    <pattern>) <operation> ;;
    <pattern-2>) <operation> ;;
    *) <for-everything-else> ;;
  esac
```

### Make an initial variable incremental loop

Sometimes you want to create a loop where you **start with a counter variable**
and **keep adding** or perform some operation on it **until it reaches some
condition**

For that there is a **special syntax**.

- **First expression**: Initial settigns **before the loop** starts
- **Second expression**: Condition to **evaluate after each loop**
- **Third expression**: Operation to **do before each loop ends**

```bash
  for ((i=0; i<10; i+=1)); do
    echo $i
  done
```
