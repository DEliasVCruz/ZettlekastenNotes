# lang.c.bitwise_operations

Manipulate individual bits in a variables value

## Synopsis

```c
char flags = 0x01 | 0x02 | 0x03
```

## Overview

This are operands that let you perform boolean logic
over every bit of a variables value, resulting in a
new value for each bit based on the boolean logic
being used

- They are most commonly used for [bitmasking](./1w01.md) 

## Cookbook

### Bitwise AND, OR, XOR and NOT

You can do all the basic boolean opeartions

- **AND**: Operator `&`
  - Ex. `0x00 = 0x01 & 0x00`

- **OR**: Operator `|`
  - Ex `0x01 = 0x01 | 0x00`

- **XOR**: Operator `^`
  - Ex `0x00 = 0x01 ^ 0x01`

- **NOT**: Operator `~`
  - Ex: `0x01 = ~0x00`

They can also be used with the assigment shorthand
syntax

- So `a &= b` it's equal to `a = a & b`

### Bitwise Shift

It consists of adding extra zero bits at the end or
the beginning of a binary number

So you have **two operands**, that both have to be some
`integer` type, one (left) that will represent the binary 
value you want to shift and the other (right) that 
represents the amount of zeros you want to add to the 
end of it

> Before doing any shiftitng the compiler will promote
> both operands to an `integer` type of the same type
> and so the type of the result will be the type of
> the promoted left operand

- **Shift left**: Operator `<<`
  - Ex: `0x02 = 0x01 << 1`

- **Shift right** : Operator `>>`
  - Ex: `0x01 = 0x02 >> 1`

You can also use the **assigment shorthands** with
them

- So `a <<= b` it's equal to `a = a << b`

> You can't perform negative shifts, and no shifts that
> are larger than the size of the promoted left operand
> other wise it will result in `undefined` behaviour

You can however shift a `signed int` just make sure it's
a positive one
