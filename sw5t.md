# cli.bc

Arbitrary precission arithmetic calculation language

## Synopsis

```sh
bc
```

## Overview

This program is like a calculator in your terminal, but can also
function as a language to run scripts for arithmetic operations

## Options

- `-l`: Load the standard math library at startup

## Cookbook

### Enable high precision division

To enable high-precision division in `bc`, you must set the `scale` variable 
to the desired number of decimal places before performing the division.

> You can also start the program with the `-l` flag to load the standard 
> math library, which sets the default `scale` to `20`

By default, bc has a scale of `0`, resulting in integer arithmetic. For example, 
to get `10` divided by `3` with two decimal places, you would set `scale = 2` and 
then calculate `10 / 3`, which yields `3.33`.

```bc
# Start bc and set scale to 5
scale = 5

# Now perform the division
10 / 3
3.33333 # The result is displayed with 5 decimal places
```
