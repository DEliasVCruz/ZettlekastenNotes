# lang.regex

A pattern that is matched against a subject string from left to right

## Overview

Regular expressions are **used** to **replace text** within a string,
**validating** forms, **extracting a substring** from a string **based on a
pattern** match, and more.

## Meta characters

They are the **building blocks** of regular expressions. Some of them **have
special meanings** and are written **inside square brackets**

- `.`: **Period** matches **any single** character **except line break**

- `[]`: Matches any **character** contained inside a **single time**

- `[^]`: Matches any character **not inside** it, a single time

- `*`: Matches **0 or more repetitions** of the symbol before it

  - This means that **if the symbol** is not **in the matched expression** it
    will **still match it**

- `+`: Matches **1 or more repetitions** of the symbl before it

- `?`: Matches **0 or 1 repetitions** of the symbl before it

  - It can **also work on other modifiers** like `(.*?at)`, which means match
    anything up to `at` but **no more than one time**

- `{n,m}`: Matches at least "n" but not more than "m" repetitions of the symbol
  before it

- `(xyz)`: Matches the character "xyz" in **that exact order**

- `|`: Matches either the **character/expression before or after** the symbol.

  - Alternation **functions as an OR** statement and **works** at the
    **expression level**

- `backslash`: **Escape** especial character to **use them literally**

- `^`: Matches the **begining of a line**

- `$`: Matches the **end of a line**

## Shorthands

- `\w`: Matches **alpha numeric** characters `[a-zA-Z0-9_]`
- `\W`: Matches **non-alphanumeric** characters `[^\w]`
- `\d`: Matches **digits** `[0-9]`
- `\D`: Matches **non-digits** `[^\d]`
- `\s`: Matches a **whitespace** character
- `\S`: Matches **non-whitespace** characters `[^\s]`

### Basic Matchers

#### The Full Stop

In regex `.` works similiar to the `?` **glob** as it will only match **any one
single character** including spaces but not newlines

For example, `.ar` will match **car**, **par**ked and **gar**age

#### Character Sets

They are **specified** by `[]`, use a `-` in between characters **inside** the
breckets to **specify the range**

This regex `[Tt]he` will match **The**, **the**, T**the** and t**The**re

So the **order** of the characters **inside** the brackets **don't matter** what
**matters** is the **order in the matched string**

But a period means a **literal period**. The following `ar[.]` will match
c**ar.** but not "ara"

#### Capturing Groups

If we put a **qualifier after a capturing group** it will **repeat** the
**whole capturing group**

For example, to match **zero or more repetitions** of the string `ab`

```regex
  (ab)*
```

We can also use **alternation** meta character `|`. For example, to **match** a
**lowercase** `c`, `g` or `p`, **followed** by `a`, **followed** by `r`.

Thou you could **achive the same result** using `[cgp]ar` which will **take
less steps**

The advantage is that this **not only matches** but **also captures** the match
to **be used by a parent language** like python or any other

```regex
  (c|g|p)ar
```

#### Non Capturing Groups

A capturing group that **matches the character but does not capture the
group**. It is denoted by **beginign** the group **with** a `?:`

They can be **usefull** in **find-and-replace** functionality or when **mixed
with other** capturing groups

For example this will be **similar** to `(c|g|p)ar` **but will not capture the
match**

```regex
  (?:c|g|p)ar
```

#### Look Arounds

They are expression that are **not part of the final match** but indicate that
the matching expression has to **either be or not be preceed or followed** by that
expresion

They work inside **capturing groups** `(...)`

- `?=`: What the expression **must be followed by**
- `?!`: What the expression **must not be followed by**
- `?<=`: What the expression **must be preceed by**
- `?<!`: What the expression **must not be preceed by**

In this example the look around **ensures** that the expression **must be
followed by** a whitespace and the word "fat"

```regex
  (T|t)he(?!\sfat)
```

## Cookbook

### Negate a set of characterss

**Preceding a character inside brackets** with an `^` will match **any character
except** it

**Any** character **except** `c`, **followed by** the character `a`, followed
by the letter `r`.

```regex
  [^c]ar
```

### Match any number of lowercase letters in a row

```regex
  [a-z]*
```

### A string surronded by 0 or any number of spaces

```regex
  \s*cat\s*
```

### The string should have at least one instance of any character

Here is matching **from the first** `c` **to the last** `t` on the sentence

```regex
  c.+t => "cat sat on the mat"
```

### Specifiy a minimum number of repetitions

This will match 2 or more digits

```regex
  [0-9]{2,}
```

### Match an exact number of instances

This will match **exactly 3 digits**

```regex
  [0-9]{3}
```
