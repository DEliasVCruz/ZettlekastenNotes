# cli.git.clean

Removes all untracked files from the git working directory

## Synopsis

When you have a set of newly added files that have not yet been
tracked by `git` by being [staged](./r03e.md) and [commited](./nr07.md) that
you want to remove from the working tree

```sh
  git clean -fd
```

## Overview

This removes all untracked files from the `git working tree`. Be sure
keep in mind the implications of running this `command`

- Deleted untracked Git files **cannot be recovered**
- Always do a **dry run first** before you remove untracked Git files

It also won't remove the following type of files

- Tracked files
- Files that are part of an existing `commit`
- Files that have been `staged` (added to the `index`)
- New directories (by default)
- Files listed in the `.gitignore` file (by default)

## Options

- `-f`: Forces the removal and ignores directories and ignored files
- `-n`: Performs a dry run of the files to be removed
- `-d`: Forces the removal of untracked directories
- `-x`: Removes untracked files that map to `.gitignore` entries
- `-i`: Interactively remove untracked files

## Cookbook

### Remove untracked files

> Remmber that you can accomplish a similar thing in a safer way
> with a [stash](./6z2q.md) `push` and the `--include-untracked` flag

The command can only be used when either the `--force` or `--dry-run`
flags are provided, so it can't be used on it's own

For safety reasons you should try to perform a `dry run` before
executing the full `clean` command

```sh
  git clean -n
  # Review to be removed files

  git clean -f # Removes untracked files
```

### Remove untracked directories

By default untracked directories and it's recursive elements wont't be
removed by the `clean` command alone, for that you'll need to aditionally
suply the `-d` flag

```sh
  git clean --dry-run -d
  # Review to be removed files

  git -fd # Removes untracked files and directories
```

### Remove ignored files

You can also force it to remove all the files cover by the `.gitignore`
file with the `-x` flag

```sh
  git clean --dry-run -x
  # Review to be removed files

  git -fx # Removes untracked files and ignored files
```
