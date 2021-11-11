# lang.bash.oper.conditional

Conditional statements structure and particularities in bash

## Synopsis

```bash
  if [[ condition ]]; then
    <operations>
  elif [[ condition ]]; then
    <operations>
  else
    <operations>
  fi
```

## Overview

The **condition** has to be **defined** with the [special character](./tmd3.md)
`[[ ]]`, since this **evaluates an expression** (`true` or `false`)

The **condition** has to **come with** a `;` right **after it**

## Cookbook

### Evaluate a conditional expression

When using an `if` statement you want to **specified a condition**, usually in
the form of **value comparison** with only **one equal** (`=`)

```bash
  if [[ "$drop" = "" ]]; then
      drop=$1
  fi
```

### Evaluate a mathematical expression

If we are **evaluating a mathematical expression** we must **use** `(( ))`
**instead of** `[[ ]]` and **double equal** (`==`) for **value comparison**

```bash
  if (( (("$1" % 3)) == 0 )); then
      drop=${drop}Pling
  fi
```

### Exit a conditional statement prematurely

You can use the **builtin command** `exit` to **escape out** of a conditional
statement prematurely, you can also provide an [exit status](./wokn.md)

```bash
  if [[ condition ]]; then
    <operation-on-succes>
  else
    exit 1;
  fi
```

### Group statements together

You can **group different statements** to function as **one unit** with the
**special character** `{ }`.

Whatever is contained inside is **treated as one** single **combined
statement**

Remember you **need a semicolon or newline before** the closing curly brace

```bash
  if [[ condition || { condition && condition; } ]]; then
    <operations>
  fi
```

### Apply comparison operands on numbers

Camparison operators (=, !=, >, and <) **only work when comparing strings**. If
you want to **compare numbers** there is a **different set of operators**:

- `-eq`: **Equals**, same as "="
- `-ne`: **Not equals**, same as "!="
- `-lt`: **Less than**, same as "<="
- `-gt`: **Greatter than**, same as ">"
- `-le`: **Less or equal than**, same as "<="
- `-ge`: **Greater or equal than**, same as ">="
