# lang.c.pointers

A variable that stores the reference to the memory location of a value

## Synopsis

```c
char *hello = "World";
```

## Overview

A pointer is an **`integer` variable** that holds a **memory address** that **points**
to a **value**, instead of holding the actual value

The computer memory is a sequential store of data, and a pointer points to
a specific part of memory. We can use pointers to point to a large amount
of data of memory, and decide how much we want to read from that point on

## Cookbook

### Dereference a pointer

You can use `*` operator to dereference a pointer and the `&` operator to
get the pointer reference of a value

```c
int a = 1;
int * pointer_to_a = &a;

a += 1;

*pointer_to_a += 1;

// This will be equal to "3"
printf("The final value is %d\n", a)
```
