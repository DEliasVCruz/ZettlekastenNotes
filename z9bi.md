# cli.git.reset

This sub-command can help you **unstage files from your staging area** this
**will not restore** them to their **previous form**.

## Overview

It can also **move the branch reference to a different commit** and **undo a
bad commit**. When **used without flags** it will **not update index**

## Synopsis

```sh
  git reset [-flags] [files|commits]
```

## Options

- --hard: Move branch to a different commit and **update working tree**
- --soft: Move branch **don't update working tree** and **keep changes staged**

## Cookbook

### Reset the current branch HEAD to the commit you specify

This is how to **make a branch point to a different commit**. Here you are also
[checking out](./it3j.md) the commit; so the files are changed to the way
they were in thta commit.

```sh
  git checkout <branchname>
  git reset --hard <commitid>
```

This way of [moving branches](./j4in.md) around is dangerous since all changes
and commits thta were made after the that point will be removed and lost. **So
be carefull!**

### Undo a bad commit and fix a commit

This is how to **correct a mistakes you made on a commit** but without making a
new commit on top of the bad one, this will **move the branch** to a previous
commit but **don't update working directory**

Using the `--soft` flag will keep the **changes as staged**

```sh
  git checkout <branchname> # Move to the branch you want to reset
  git reset <commitid> # Make the branch point to a different commit
```

This is **recommended when working with local repos** if you want to **revert
commit** that you have **already pushed** to a remote branch **your best option
is** [revert](./36re.md)

### Unstaging a file

Although you can use `reset` to remove a file from the staging area
it is not recommended since it can have unintended consequences

```sh
git reset HEAD <filename>
```

It's better to use the [restore](./8m7k.md) command for this operation

```sh
git restore --staged <file-to-unstage>
```

### Restore a file to it's original or previous version

For this you may want to use [checkout](./it3j.md) to bring back a version of
the file from a previous commit 

```sh
  git checkout [<commitid>] <[deleted]file>
```

Or [restore](./8m7k.md) to remove unstage changes from the index

```sh
  git restore <file>
```

