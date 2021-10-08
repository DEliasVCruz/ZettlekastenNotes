# cli.git.reset

This sub-command can help you **unstage files from your staging area** this
**will not** [restore them to their previous form](./8m7k.md).

## Overview

It can also **move the branch reference to a different commit** and **undo a
bad commit**.

## Synopsis

```sh
  git reset [-flags] [files|commits]
```

## Options

- --hard: Move branch to a different commit

## Cookbook

### Reset the current branch HEAD to the commit you specify

This is how to **make a branch point to a different commit**. Here you are also
[checking out](./it3j.md) the commit; so the files are changed to the way
they were in thta commit.

```sh
  git checkout <branchname>
  git reset --hard <commitid>
```

### Undo a bad commit and fix a commit

This is how to **correct a mistakes you made on a commit** but without making a
new commit on top of the bad one, this will move the branch to a previous
commit but don't update working directory

This is **recommended when working with local repos** if you want to **revert
commit** that you have **already pushed** to a remote branch **your best option
is** [revert](./36re.md)

```sh
  git checkout <branchname>
  git reset <commitid>
# make changes to files
# stage and commit
```

### Unstage files

```sh
  git reset [<commitid>|<branchname>] <files>
```

### Restore a file to it's original or previous version

For this you may want to use [checkout](./it3j.md) the file
