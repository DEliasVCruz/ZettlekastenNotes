# cpt.encoding.binary

How the binary encoding works

## Overview

Binary is an encoding mechanism that consists of only two symbols
which are `0` and `1`, due to it's simplicity pretty much anything 
can be encoded in binary and can be transmitted in a variety of
ways (like light pulses)

Where as in a `base 10` system each character in the value
represent the number of times that a power of ten is repeated

> 72 = 7 * 10^1 + 2 * 10^0

As a `base 2` number system each character in the binary value
represents a power of `2`

> 101 = 1 * 2^2 + 0 * 2^1 + 1 * 2^0 = 72

We can see this visually if we expand it for the possibility of
representing number with up to `8 bits`

> 128  64  32  16  8  4  2  1
>   0   0   0   0  0  1  0  1

Thus for an `8 bit` binary allocation we can represent up to the
number `255`

> 128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255

## Cookbook

### How to represent a value as binary

In many programming languages they will give you the ability
to represent a value as it's binary encoding, usually by
prefixing the binary value with `0b`

```c
int myNumber = 0b00000001 // This is number one
```

### How to get the binary representation of a number

You can get the binary equivalent of a number by continuously
dividing it by `2` and keeping the remainder

In this case the binary representation of `72` is `1001000`

> 72 / 2 = 36 r 0
> 36 / 2 = 18 r 0
> 18 / 2 = 9  r 0
> 9 / 2 = 4   r 1
> 4 / 2 = 2   r 0
> 2 / 2 = 1   r 0
> 1 / 2 = 0   r 1

### Get the value of a binary number when multiply/divided by `2`

If you multiply a binary number by `2` then it would be equal
to just adding a `0` to the end of the binary value

> 72 = 1001000
> 144 = 10010000

In the same vein if you wanted to divided by `2` then it would
equal to removing a `0` from the end

> 72 = 1001000
> 36 = 100100
