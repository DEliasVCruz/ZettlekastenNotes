# cli.py.debug.pdb.inspect

Inspect the results of arbitrary expressions

## Synopsis

```pdb
  (Pdb) p
```

## Overview

You can inspect the results of arbitrary `Python` expression, **such as
variables**, through the execution of your code

## Cookbook

### Printing the results of an expression

You can print the **results** of **any valid** `Python` **expression** with the
`p` command, this **includes**:

- **Variable names**: By passing the name of the variable
- Any valid `Python` expression you would use in your source code

You can also use the `pp` command to **pretty print** the output of expression
that may include more than one line

```pdb
  p my_variable
  p 'This is the value: ' + my_variable
  p [x + 2 for x in my_list]
```

### Print the argument list of a function

You can **list all** the **arguments** of a **function** and their **current
values** with the `a` command

```pdb
  a
```

### Watch/Follow the result of an expression

You can use the `display` command to **print** the **result** of a `PYthon` **expression
every time** a **execution** of the code **stops**

You can use this to **watch variables**, if it changed, every time you step
through code

```pdb
  (Pdb) display my_variable
  dispaly my_variable: 'a_value'
  (Pdb) n
  dispaly my_variable: 'another_value' [old: 'a_value']
```

You **can only pass one expression at a time**. So if you want to watch many
expressions you need to pass them one by one and **then call** `display`

```pdb
  (Pdb) display my_variable
  display my_variable: 'value1'
  (Pdb) display another_variable
  display another_variable: 'value2'
  (Pdb) display final_variable
  display final_variable: 'value3'

  (Pdb) b my_file:11
  (Pdb) c
  (Pdb) display
  Currently displaying:
  my_variable: 'value1'
  another_variable: 'value2'
  final_variable: 'value3'
```

To **stop following an expression** you can use the `undisplay` command and pass
the expression

```pdb
  (Pdb) undisplay my_variable
```

### Print current context code

You can use `ll` (long list) to print the current context (function definition)
or `l .` to print the 11 lines around the current line (you need to **pass the
dot argument**)

```pdb
  ll
  def my_func():
      pass

  l .
  <11 lines around current line>
```
