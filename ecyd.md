# cli.git.reflog

Reflog allows you to **go back to commits** even though they are **not
referenced by** any **branch or tag**.

## Overview

Every time your **branch tip is updated** for any reason (by switching
branches, pulling in new changes, rewriting history or simply by adding new
commits), a **new entry will be added to the reflog**.

The reflog **contains information about the old state of branches** and allows
you to **go back to that state if necessary**.

This references can be later **used in place of** the traditional **commit
hash** in any other **git command**.

## Commands

- show: Select what reference to use

## Options

- --all: Select all references
- --relative-date: Shows relative date information

## Synopsis

The **syntax** to **acceess** a **git ref** is `name@{qualifier}`.

```sh
  git reflog [default=HEAD|<branchname>|name@{qualifier}]
```

## Cookbook

### How to see the commits you've jumped to before

See a reference **log of the commits you've checkedout**. By default this is
short for `git reflog show HEAD`

```sh
  git reflog
```

### Show all commits that reference a specific branch

```sh
  git reflog show <branchname>
```

### Use reference pointers in other git commands

You **pass the reference pointers to any git command** that would accept sha1
commit hashes

The following example display Git diff output comparing the `stash@{0}` changes
against the `otherbranch@{0}` ref.

```sh
  git diff stash@{0} otherbranch@{0}
```

### Show changes that have occurred within a time frame

Every reflog entry has a timestamp and this can be used as a **qualifier**
token of the **reflog syntax**. With this we can **filter by time**.

This are examples of available time qualifiers:

- 1.minute.ago
- 1.day.2.hours.ago
- yesterday
- 1.week.ago
- 2.months.ago
- 1.year.ago
- 2021-05-17.09:30:25

This example will **diff the current main branch against main 1 day ago**.

```sh
 git diff main@{0} main@{1.day.ago}
```

### Recovering lost commits

Git never really loses anything, even when performing history rewriting
operations like [rebasing](./7ddq.md) or [commit](./nr07.md) amending.

In this example we have made some interactive rebasing and **squashed** some
commits together. If we examine [git log](./m36a.md) it **appears** that we
**no longer have the commits** that were marked for squashing.

If we then want to **operate on the squashed commits** we can use `reflog` to
reference those commits.

```sh
  git reflog
```

After this we will there are **reflog entries for the start and finish of the
rebase** and prior to those is our **squashed commit**. We can pass the reflog
ref to git [reset](./z9bi.md) and **reset to a commit that was before the
rebase**.

This will essentially **restore the other squashed commits**.

```sh
  git reset reference@{qualifier}
```
