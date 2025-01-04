# cli.nm

List symbol names in object files

## Synopsis

```sh
nm [<options>] <path-to-object-file>
```

## Overview

You can use this to show the symbols that come with
an object file, in a list format

For each symbol it shows:
  - The symbol value (in [hexadecimal](./4gzy.md) by default)
  - The symbol type
    - I lowercase, the symbol is usually local
    - If uppercase, the symbol is global (external)
    - (`u`, `v` and `w`) are special global symbols 
      that use lowercase
  - The symbol name

## Options

- `-g`: List only the global (external) functions
- `-u`: List only undefined symbols
- `-a`: List all symbols, including debugging symbols
- `--demangle`: Demangle `c++` symbols

## Cookbook

### See the symbols packed with an object file

For this, you can use `nm` directly on an object file

```sh
nm path/to/file.o
```

### Find the mining of the type letters in the symbols

You can review the `man` pages for `nm` to see the list of
types used, and what they represent

> Other symbol types not listed in the `man` pages might
> appear depending on the object file format

### Demangle `c++` symbols

When you create an object fiile from a `c++` file, the
names of the functions get **mangled**, which means they
add some prefixes and suffixes to support some of their
features like function overloads

This meaks the symbols very hard to spot and read, you can
use the `--demangle` flag to make the symbols readable
again

> You can pass a `mangling` style argument to the option
> to specify a particual compiler `mangling`

```sh
nm --demangle[=style] path/to/file.o
```
