# cli.go.test

Built in go test runner, automates testing the packages

## Synopsis

```language
  go test [build/test flags] [packages] [build/test flags & test binary flags]
```

## Overview

## Cookbook

### Don't use the cache when running test

You can force not using the `cache` when runnig test by three
main ways

- Using the [clean](./x0a7.md) command

```sh
  go clean -testcache
```

- Using a `non cacheable` flag with the test command

```sh
  go test -count=1 .
```

- Regular changes to source files will invalidate the
  cached test results
