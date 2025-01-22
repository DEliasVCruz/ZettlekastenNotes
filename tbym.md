---
tag: ["buildsystem"]
---

# cli.make



## Synopsis

```language

```

## Overview

## Cookbook

### Set default target to run

By default when invoking `make` alone it will try to **make** 
the top most **recipe** in your `Makefile`

If you want it to run some other recipe by default you
can specify it with `.DEFAULT_GOAL`

> This will make `run` when calling only `make`

```makefile
.DEFAULT_GOAL := run

build: main.go
  go build -o main main.go

run: build
  ./main
```

### Set a target as non producible

Though `make` can be use as a sort of command runner
it's primary purpose is not really that, but to
make `targets` based on `dependencies` and `recipes`
on how to **make** those targets

However it's common to use `make` as a command runner
and so in cases when the command it's equal to
a `target` that has been already made and it's
dependencies haven changed, then `make` won't build
them again

This can be problematic in the for example a case
where you have a `recipe target` called `test` but
you also have some file called `test`

For this case you can mark the `target` as `.PHONY`
to tell `make` that it's OK to run this again since
it does not map to a real `target`

```makefile
.PHONY build
build: main

main: main.go
  go build -o main main.go

.PHONY clean
clean:
  go clean
  rm build
```
