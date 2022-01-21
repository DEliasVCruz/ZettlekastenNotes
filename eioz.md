# cli.py.pip

The standard built-in package manager for Python

## Synopsis

```sh
  pip [<flags>] [<comands>] [<packages>]
```

## Overview

It is **best practice** to run pip with `python -m pip` to **ensure** you are using
your **current python's** version of **pip**.

## Cookbook

### Upgrade a package

You can do so **usign** the `install` command with the `--upgrade` flag

```sh
  pip install --upgrade [<package>]
```

You can **upgrade pip** the same way

```py
  pip install --upgrade pip
```

### Get info about a package

With the `show` command you can **display metadata** about a package such as:

- The **package dependencies**
- What other **packages depend on it**
- **Location** in your `Pythoh` \$PATH
- **Author** of the package
- **Version**

```sh
  pip show [<package>]
```

### Uninstalling a package

When you unistall a package with pip it **does not automatically unistall** it's
**unsed dependencies** as well

So you need to **manually unistall** them if you so desire with the `unistall`
command and the `-y` yes flag

```py
  pip uninstall -y urllib3 chardet idna requests
```
