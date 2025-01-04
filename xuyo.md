# cli.git.diff

Used to view **what changes you've made to files**. In the form of **lines
added and lines removed**

## Overview

The default behaviour checks current unstaged changes against the current
[commit](./nr07.md)

## Synopsis

```sh
  git diff [options] [<commitid> [<commitid>]]
```

## Options

- --staged: Compares staged changes against an specified commit (defaults=current)

## Cookbook

### Check unstaged changes

To see what **changes** you have made but **not yet staged** since de last commit

**If** there is **already staged changes to the file**, then it **diffs it
agains the staged changes**

```sh
  git diff
```

### Check changes between specified commits

To see **what has changed from one commit to another**

It will show you **what has to be added or removed from the first specified
commit to equal the second specified commit**

```sh
  git diff <commitid> <commitid>
```

### Get a list of only the files containing merge conflicts

When wanting to see only the files that have merge conflicts
you can use the following options:
  - `--name-only`: Show only the file names
  - `--diff-filter`: Filter the diff by some criteria in this case
    - `U`: For unmerged or conflicted changes

```sh
  git diff --name-only --diff-filter=U
```

### Check changes made from a previous commit to the lastes one

```sh
  git diff <commitid> HEAD
```

### Compare staged changes agains an specified commit

This **defaults to the current commit**

```sh
  git diff --staged [<commitid>]
```

### Use an external difftol

```sh
  git difftool --tool--help
```
