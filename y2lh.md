# lang.bash.type.parameter

They function like variables and can store string data, integers, indexed and
associative arrays

## Synopsis

```sh
  <varname>=<vardata>
```

## Overview

There are **two types**:

- **Variables**: You can create an update
- **Special parameters**: Preset and used to communicate internal statuses

Remember that parameters **don't start with** a `$` sign, this is the
**operator** that **prompts** the shell to **expand** the **specified
parameter**

### Variables

The **name** of a variable has to be a **word** consisting only of letters, digits
and underscores, and **beginning** with a **letter** or an **underscore**.

When assigning a variable you **cannot use spaces around** the `=` sign. Since
it will threat `<varname>` as a [command](./rffs.md) with `-` and `<vardata>`
as it's arguments

```sh
  # This is wrong!
  varname = vardata
```

If you want to achieve this behavior by using the `(( ))` [special
character](./tmd3.md)

```sh
  (( <varname> = <vardata> ))
```

#### Types of Variables

Bash is **not a typed language** but variables can be **defined** with
**limitations** on the type **of content** they are allowd to have

**DECLARING VARIABLES THIS WAY IS RARE**!

- **Array**:

  - The variable is an array of strings
  - Defined as `declare -a <array-name>=<array-data`
  - It is **suficient** to write `array=(...)`

- **Associative array**::

  - Like a **dictonary**
  - Defined as `declare -A <associative-array-name>=<data>`

- **Integer**:

  - This automatically triggers **Arithmetic Evaluation**
  - Defined as `decalre -i <varname>=<integer>`
  - Can **also** be defined as `let <varname>=<integer>`

- **Read Only**:

  - It can **no** longer be **modified or unset**
  - Defined as `decalre -r <varname>=<vardata>`

- **Export**:

  - It will be **inherited** by any child process
  - Defined as `decalre -x <varname>=<vardata>`

### Special parameters

Here is a summary of most of the _Special Parameters_:

- `"$0"`: Contains the name, or the path, of the script
- `"$1"`: Contain the arguments that were passed
- `"$@"`: Expands to all the words of all the positional parameters
- `$#`: Expands to the number of positional parameters
- `$?`: Expands to the **exit code** of the most recent completed command
- `$$`: Expands to the process ID number of the current shell

The ones that have **quotes** around them are **meant to be used like that**

- **Positional parameters**:
  Are **references to** the **passed arguments in order** so the **first** passed
  argument **will** be `"$1"`, the second `"$2"` and **so forth**

## Cookbook

### Access the data stored in a variable

You can use [parameter expansion](./2zqa.md) to **substitute** the parameter **by
it's value**. After that, you may perform **additional manipulations** on the
**result**

```sh
  foo=bar
  echo "Foo is $foo"
```

### Use a variable that contains white spaces

Remember that it will **replace** `$<varname>`, then perform **word splitting**
and **only THEN** execute a command

So if your **variable** has **white spaces**, bash will read each
[substring](./n08y.md) as an argument for your **command**

The following is similar to `rm My song.mp3`

```sh
  song="My song.mp3"
  rm $song
```

The way we fix this is by **putting double quotes around every parameter
expansion**

This way the following is similar to `rm "My song.mp3"`

```sh
  song=""My song.mp3""
  rm $song
```

## Use passed arguments in your function or script

To **reference** the **arguments** provided by the user inside your function or
script you can use the **special positional parameters**

## Call a function with all the positional parameters

When you are **using** a **function inside a script** you need to call that
function and **pass the** positional parameters as **arguments**

If you wanted to pass **every** positional **parameter** provided by the user **as
arguments** to your `main` function you would:

```sh
  main $@
```

## Concatenate two variables

There is **no explicit concatenation operator** for strings. You just **write
them adjacent to each other**

```sh
  var=$var1$var2
```

**If** the right-hand side **contains white space characters**, it **needs** to
be **quoted**:

```sh
  var="$var1 - $var2"
```

You can **append a string** to a variable by using **curly braces**(`{ }`) or
**quotes** to **disambiguate** the right-hand side. Without this the **string**
will be **interpreted** as part of the **variable name**:

```sh
  var=${var1}xyzzy
  var="$var1"xyzzy
```

### Increment a variable by itself

Just like in python if you are going to **redifine** a variable by
**incrementing it based on itself** you can use the `+=` operator

```bash
  counter=0
  ((counter+=1))
```

### Decrease a variable by itself

The inverse operation can be made with a special `--` operator **at the end of
the variable**

```bash
  counter=0
  ((counter --))
```

## Defining variables as integers

Here is an example of how variables behave under **different types** of
**declarations**

```sh
  a=5; a+=2; echo "$a"; unset a # Results in 52
  a=5; let a+=2; echo "$a"; unset a # Results in 7
  declare -i a=5; a+=2; echo "$a"; unset a # Results in 7
  a=5+2; echo "$a"; unset a # Results in 5+2
  declare -i a=5+2; echo "$a"; unset a # Results in 7
```

Thou most shell scripters prefer to **use explicit arithmetic** commands (with
`((...))` or **let**)
