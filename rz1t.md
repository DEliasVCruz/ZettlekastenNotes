# cli.fzf.syntax.matching

Fzf supports fuzzy matching but if you **don't want fuzzy searching** and
instead you **want exact match**.

## Overview

You can **use this modifiers in between your fuzzy search**

## Magic characters

- ': Search for an exact matching
- ^: Search for the begining of a string
- \$: Search for the end of a match
- !: Serach for not include matching
- \*\*: Trigger fzf on a filepath

## Cookbook

### Make an exact search

For that you **prefixed your search with '**

```sh
  'searchedstring
```

### Match the start and end of a string

To match the **start of a string use ^**

```sh
  ^searchedstring
```

To match the **end of a string use \$**

```sh
  searchedstring$
```

### Negate matching

To get the **opposite of a match string**

```sh
  !searchedstring
```

### Fuzzy complete a filepath on the shell

Here `command` referes to any shell command like `nvim` or `cd`, one wil give
you files and dirs and the other only dirs; and `FUZZY_PATTERN` **is optional**

```sh
  command [DIRECTORY/][FUZZY_PATTERN]** # Press 'TAB' to expand in fzf
```

### Kill a process

You can fuzzy **search a procces id and kill it**

```h
  kill [signal] <TAB>
```
