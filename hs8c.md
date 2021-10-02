# cli.git.tag

You may want sometimes to **tag some of your commits** for when you've reached a
special milestone (version update) or any other memo.

## Overview

Tags are **not** `pushed` **or** `pulled` **automatically** whit remotes

## Synopsis

```sh
  git tag [options] <tag-name> [<commit-id>](defaults to <current-commit>)
```

## Options

- -d: Delete a tag
- -l: List all tags
- -a: To create an annotated tag
- -m: Define the message for the annotated tag
- -s: Create a signed and annotated tag

## Cookbook

### Tag a commit

```sh
  git tag <tag-name> [<commit-id>]
```

### Delete a tag

```sh
  git tag -d <tag-name> [<commit-id>]
```

### Push tags to a remote

```sh
  git push <remote> <tag-name>
```

**To push all your tags:**

```sh
  git push <remote> --tags
```

### Deleting tags on remotes

```sh
  git push <remote> --delete <tag-name>
```

### Sync your tags with remotes

```sh
  git fetch <remote> --prune --prune-tags
```

### Create an annotated tag

```sh
  git tag -a <tagname> -m <message>
```
