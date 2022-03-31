# cli.git.submodule

This is a way to link together different git repositories

## Synopsis

```sh
  git submodule [command] [options]
```

## Overview

Sometimes you may have a repository that may need to **reference** or use files
contained on a different and **independent git repository**

You can use `submodules` to link together this repositories inside a central
repository

## Cookbook

### Add a git submodule to your repo

Adding a submodule is simple and you just need the `url` **to the git repo**
that will be referenced as a submodule

```sh
  git submodule add <git-repo-url> <name>
  git add <name>
  git commit
```

### Clone a git repo with submodules

When clonning a repository, `git` does not automatically pull it's
`submodules`. You would have to do this mannually

```sh
  git clone <git-repo-url>
  git submodule update --init --recursive
```

### Update submodules

If a change is made to the referenced repository of `git submodule`, this will
not be automatically reflected on your repo

- You will need to manage it **as any other git local repository**

```sh
  cd <name>
  git fetch
  git merge origin/master
```

- If you need to update many submodules you can also

```sh
  git submodule update --remote --recursive
```

### View the satus of a submodule

To check on the status of all your submodules when running [git
status](./i0ps.md) you need to **configure** your `git` to this by default

```sh
  git config status.submodulesummary
  git status
```

### Delete a submodule

To delete a submodule you shuold:

1. Remove references to the `submodule`
2. Remove the directory from your repo
3. Remove the hidden reference in the `.git` root directory

```sh
  git submodule deinit <name>
  git rm <name>/
  git commit
  git push
  rm -rf .git/modules/<name>/*
```
