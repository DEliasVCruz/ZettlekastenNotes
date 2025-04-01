# cli.git.checkout

It's a git sub-command that lets you move between **branches** and **commits**

## Overview

You would use this command when you want to **switch** to a **different**
[branch](./j4in.md) or [commit](./nr07.md)

## Synopsis

```sh
  git checkout [<ommitid> | <branchname>]
```

## Options

- `--detach`: Move to the last commit of a branch
- `-b`: Create a new branch and move to it
- `--conflict`: Discard a conflicting file without discarding the whole merge process

## Cookbook

### Move down on the commit history by one

You can move back to one commit before with:

```sh
  git checkout HEAD^
```

### Move down on the commit history \#n times

You can move back an specified **\#n** number of times with:

```sh
  git checkout HEAD~<n>
```

### Move to the last commit of a branch

This **not necessarily is the one that head points to** but just the last
commit associated to that branch

```sh
  git checkout --detach <branchname>
```

### Restore to a previous version of a file (version in a past commit)

- With this **you can**:
  - **Unstage changes** to a file by checking it out
  - [Restore](./8m7k.md) **a file back to a previous version** of it in a past commit
  - **Bring back deleted files**
  - Effectively **reset a file back to it's original state**

```sh
  git checkout [<commitid>] <[deleted]file>
```

### Remove the changes done to a modifed file

If you want to discard the changes to a file in the working
directory, meaning you want to unmodify a file. You can use the
`cheout` command to do so

```sh
git checkout -- <file>
```

### Jump to a previously checked out branch

You can quickly checkout back to the last branch you were
checkedout to by pasing `-` to either the `checkout` or
`switch` command

```sh
git [checkout|switch] -
```

### Create and move the new branch

You can use the `-b` option to both switch to another and create it if it does
not yet exit

```sh
  git chekcout -b <new-branch-name>
```

### Create and move to a local version of a remote branch

You can also use the `-b` option to create a local version of a remote branch
and move to it

```sh
  git fetch --all
  git checkout -b <local-branch-name> <remote-branch-name>
```
