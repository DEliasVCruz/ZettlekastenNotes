# cpt.encoding.hex

How the hexadecimal encoding works

## Overview

`Hex` is a `base 16` number system, which means unlike the
usual `decimal` system it uses `16` symbols before having
to add an extra symbol

> 0 1 2 3 4 5 6 7 8 9 a b c d e f

## Cookbook

### Representing binary `byte` values as `hex`

Since every `byte` is equal to `8 bits` it gets cumbersome to
work with this enconding when we are trying to represent
large number of `bytes`

Thus, most binary, is often represented as it's `hex` 
encoding

This is done by separating the group of `8 bytes` into two
groups of `4 bytes` and each of thos values is transform
into a `hex` symbol

> 101 = 0b01100101 // as an 8 bit integer
> hex(0110) and hex(0101) = 6 and 5
> 101 = 0b01100101 = 0x65

In this way each `byte` can be represented as a two digit
hex number

Which make it a more **space efficient** representation when
trying to store it into some data structure

### How to represent a value as hex

In many programming languages they will give you the ability
to represent a `number` value as it's `hex` encoding prefixing 
the `hex` value with `0x`

```c
int myNumber = 0x1; // This is number one
```

### Transform a decimal number into a hex number

There is a very nice formula that you can use to transform
a decimal number into a hexadecimal one

You start by taking your number and dividing by `16`, each
time your positional value (starting from `0`) will be the
remainder of your operation

Then you take your quotient and repeat the divition until
your quotient is `0`

The you concatenate the remainders as `hex` digits with the
`0` digit being the farmost right and so on

- For example for the number `1200`

Division   | Quotient | Remainder | Digit #
-------------------------------------------
(1200)/ 16 | 75       | 0         | 0
(75)/ 16   | 4        | 11        | 0
(4)/ 16    | 0        | 4         | 0

Since `11` is represented by `b` in hex, the final `hex`
value of `1200` will be `0x4B0`

### Transform a hexadecimal number into a decimal number

To transform a hexadecimal number into a decimal one, you
just have to add up the `0` started powers of `16` scale by
their digit position

- For the `hex` number `0xCC` (Consider tha `C` is `12`)

> 0xCC = (12 * 16^1) + (12 * 16^0) = 204

The decimal representation of `0xCC` will be `204`

## Sources

- Here is an online [conversion calculator](https://www.rapidtables.com/convert/number/decimal-to-hex.html?x=1200) 
