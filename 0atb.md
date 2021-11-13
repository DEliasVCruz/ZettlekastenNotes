# cli.git.push

Push your local changes an upstream remote

## Synopsis

```sh
  git push [options] <remote> <branch>
```

## Overview

To **sync** your **local changes with** the different **remotes** you may be
working with. As long as you **have write permissions** for the remote

## Options

- `--all`: Push all branches at once
- `--force`: Overwrite remote history

## Cookbook

### Overwrite the remote branch with your local changes

Sometimes you may want to **overwrite** the **history** that is **in your
remote branch**, for various reason including just rearranging the [remote](./95us.md)
history for mistakes.

Just remember that **THIS IS DANGEROUS!!!**, the **COMMITS THAT ARE OVERWRITTEN
WILL BE LOST**

```sh
  git push --force <remote> [<branch>]
```

### Push all your branches to a remote

To **push all** your local [branches](./j4in.md) **at once**

```sh
  git push --all <remote>
```

### Push your local tags to a remote

**By defaul** git **won't push** your **local** [tags](./hs8c.md) along with your
associated branch when pushing. You **have to mannually push them**

```sh
  git push --tags <remote> [<branch>]
```
