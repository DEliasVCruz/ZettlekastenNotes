# cpt.system.endianness

The way in which machines store multi byte data

## Overview

When a machine stores multi byte data such as a
`32` bit integer. It needs to decide in what order
it's going to store the consecutive bytes

This is necessary because the whole of the information
can't be packed in `8` bits, and it can't be analyzed
byte by byte either. The informatin needs to be
decoded as a whole

> Keep in mind that endianness is mostly a hardware
> concern and for most developers on the same machine
> it should not matter

For example, given a `32` bit integer expressed in
[hex](./4gzy.md) as `0xa01183d1` (which is `4` bytes), It could
store it in one of two ways

- `Little endian`: Least significant bits first
- `Big endian`: Most significant bits firsurl

### Big endian systems

In this type of hardware systems multi byte data is
layed out starting from the **most significant** byte
of the data

The **most significant byte** in this case refers to
the byte that represent what would be the most amount
of data

For example take the number `512` here the **most
significant digit**  would be `5` since it actually
represents the number `500`. And in the case of a `32`
bit integer, the first byte would represent the bits
with the higher powers of `2` in [binary](./acl6.md) 

So for the case of `0xa01183d1`, the bytes would be
stored as:
  - First byte `a0`
  - Second byte `11`
  - Third byte `83`
  - Fourth byte `d1`

### Little endian systems

In this type of hardware systems multi byte data is
layed out starting from the **least significant** byte
of the data

So for the case of `0xa01183d1`, the bytes would be
stored as:
  - Frist byte `d1`
  - Second byte `83`
  - Third byte `11`
  - Fourth byte `a0`

From the programmer perspective for most cases this 
would be of no concern since the hardware will re-arrange
them when they need to be read

The only problem would be when using a [debugger](./1nja.md) and you
are trying to inspect each individual byte of the data
since then they would be presented in their original
layout and you would need to make that adjustment your
self

### Endianness when comunicating between computers

The most common point when the endianness of a system
becomes of a concern is when 
  - Comunicating between computers
  - Reading external files or network data

Since for computer to computer comunication we need to
agree at a protocol level what will be the endianness of
used, since other wise it could lead to each some machines
interpreting the data as something completely else

And the same when reading external files or network data
since the data in the file might've been layed out by a 
computer with a different endianness, there for in most
binary formats an endianness is decided in the specifications,
so then both machines that write and read from that format
need to do their conversions if necessary

### Non multy byte data and endianness

Endianness is not relevant for data that is not multi byte,
for example in the case of [strings](./jfth.md) since, like how it is
on c, they are already represented as an array of bytes where
each character is an `8` bit number
