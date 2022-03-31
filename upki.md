# cli.pacman

Package manager for the arch operating system

## Synopsis

```sh
  [sudo] pacman [options] <package>
```

## Overview

The `pacman` program is the **default package manager** of `Arch` based distros

## Cookbook

### Get all the install packages

You can print all the **native** and **explicitly** installed packages with the
`-Qqen` option combination

- You can then **batch install** all your packages from a `requirements.txt` file

```sh
  pacman -Qqen > package_list.txt
  pacman -S - < package_list.txt
```

### Find information about a package

You can **get information about** a package with the `-Sii` option combination

```sh
  pacman -Sii <package>
```
