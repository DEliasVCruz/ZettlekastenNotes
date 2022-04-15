# cli.chown

Change file and directory user ownership

## Synopsis

```sh
  [sudo|doas] chown [optinos] <group>:<user> [<directory>|<file>]
```

## Overview

## Cookbook

### Change the owner of a file

You can use the `-c` option followed by the group and [user](./fa42.md) name to
change the ownership of a given file

```sh
  sudo chown -c root:root /etc/doas.conf
```
