# cli.py.unittest

Run your unit test modules

## Synopsis

```sh
  python -m unittest [<flags>] [<test-names>|discover]
```

## Overview

You can **run your tests** by passing the name of the modules containing your tests
directly or using the `discover` command that will run any file that has the
`test*.py` file name structure

- `discover`: Search and exsecute any file in the form of `test*.py`
- `-s <directory>`: Search for tests in the given directory
- `-t <directory>`: Directory where your source code lies
- `-v`: Display the names of the executed tests in order alogn with their result

## Cookbook

### Run a test of suits

**In this example** we run all the test files in the `tests/unit` module that has
it's source code in the `src` directory

```sh
  python -m unittest -v discover -s tests/unit -t src
```
