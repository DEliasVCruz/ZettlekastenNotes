# lang.c.loops

Doing loop operations in c

## Synopsis

```c
for (int i = 0; i < 10; i++) {
  printf"%d\n", i);
}
```

## Overview

Looping operations in `c` are very simple and standard, you
have two basic looping mechanisms

- The `while` loop
- The standard `for` loop

Both support the use of the `break` and `continue`

## Cookbook

### How to do a while loop in c

A `while` loop is pretty simple, it will run indefinitely until
the `bool` stopping condition is met

```c
while (i < 10) {
  printf("%d\n", i);
  i++
}
```

### How to do a for loop in c

The standard for loop works like any other

- A variable initialization
- A `bool` stopping condition
- What to do after each iteration

```c
for (int i = 0; i < 10; i++) {
  ...other code
}
```
