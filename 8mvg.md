# lang.c.platform.limits

Check for the limits of various types according to the platform

## Synopsis

```c
#include <limits.h>
```

## Overview

Some data types can have different limits on the values they can
hold depending on the platform where they are set

We can make use of the values set on the `limits` library to
check for this bounders based on where it's compiled

## Cookbook

### Check for the limit values of a `long`

You can use the `LONG_MIN` and `LONG_MAX` macro values to check
for the min and max value of a long in the compiled platform
there is also an `unsigned` version of the `LONG_MAX` and a
`LONG_LONG_` version

```c
#include <limits.h>

int main(int argc, char **argv) {
  if (argc < LONG_MAX) {
    printf("Is lower\n");
  }

  return 0;
}
```
