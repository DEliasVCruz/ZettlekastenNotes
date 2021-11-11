# lang.bash.oper.expansion

Parameter expansion is the substitution of a parameter by its value

## Overview

This indicates that you want to **use** the **contents** of the **variable**.
Is **achieved by prefixing** that parameter with a `$` sign

In certain situations, **additional curly braces**(`{ }`) around the
parameter's name **are required**

```sh
  echo "'$USER', '$USERs', '${USER}s'"
  # Results in 'lhunath', '', 'lhunaths'
```

## Parameter Expansion tricks

### Use default value

**If** `parameter` is **unset or null**, `word` (which may be an expansion)
will be used. **Otherwise**, it will use the **value of** `parameter`

```bash
  ${parameter:-word}
```

### Assign default value

If `parameter` is is unset or null, it will **assign the value of** `word` to
`parameter` and **then expand the substitution**

```bash
  ${parameter:=word}
```

### Use alternate value

If `parameter` is unset or null then **no value gets assign**. If it **does
have a value**, it gets **substituted** by `word`

```bash
  ${parameter:+word}
```

### Index based expansion

Expands to **up to** `length` characters of `parameter` **starting at** the character
specified by `offset` (0-indexed), but `lenght` is (1-indexed)

If `offset` is negative (use parentheses), **count backward from the end** of `parameter`

If `parameter` is `@` **or an indexed array**, the **result** is `length` **positional
parameters or members** of the array

This ends up being **similar to string splitting** in languages like python

```bash
  ${parameter:offset:length}
```

- To **get the first character** of a string:

```bash
  ${parameter:0:1}
```

- To **get the last character** of a string:

```bash
  ${parameter:-1:1}
```

### Display parameter lengt

The **length in characters** of the value of `parameter` is substituted. If
`parameter` is an array, **return** the **number of elements**.

```bash
  ${#parameter}
```
