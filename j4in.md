# cli.git.branch

You can create **branches** to move between different **versions** of your project.
They are **cheap to create and destroy**

## Synopsis

```sh
  git branch [flag-options] <branchname>
```

## Options

- `-D`: Delete an existing branch
- `-v`: See the last commit on each branch
- `-m`: Rename a branch
- `--merged`: List branches that are already merged into the current branch
- `--no-merged`: List branches that haven't been merged into the current branch
- `-l`: List only local branches
- `-r`: List or delete only remote branches
- `-a`: List both remote tracking branches and local ones

## Cookbook

### Create a new branch

You can use this command to **create** a **new non-existing** branch. This **wont
switch you into the new branch** it will just create it.

To start working on that new branch you'll first have to [switch to it](./it3j.md)

```sh
  git branch <newbranch>
```

### Delete a branch

To delete an existing branch

```sh
  git branch -D <branchname> [or multiple branches]
```

### Move to a different branch

You can move between branches with the [checkout](./it3j.md) command

```sh
  git checkout <branchname>
```

### List branches

You can either:

- List local branches only
- List remote branches only
- List all branches (remote and local)

```sh
  git branch -l     # List local branches
  git branch -r     # List remote branches
  git branch -a     # List all branches
```

### Point branch to a new commit (movin branches around)

Once you create a new branch it will **point to your current head** to make it
**point to a different commit**:

1. First `checkout` the branch
2. **While on that branch**, [reset](./z9bi.md) the branch to a **new commit**

```sh
  git checkout <branchname>
  git reset --hard <commitid>
```

After you reset your branch to a new commit. **All commits that come after this
version are effectively undone**

### Create a new branch with your stashed changes

If you want to create a new branch bsed on your [stashed](./z9bi.md) changes

```sh
  git stash branch <branchname> [<stash>]
```

### Delete a remote branch

There are a **two ways** to delete a remote branch.

First make sure that you have **deleted** your **local version of** the
**remote branch** and execute the following

```sh
  git branch --remote -D <remote-name>/<branchname>
  git push <remote> --delete <branchname>
```

Another way is to delete your local branch and the push it with a `:` to the
remote to delete it uppstream

```sh
  git branch -D branch_name
  git push origin :branch_name
```

### Rename a local branch

You can use the `-m` option to give a local branch a new name, this **will not
make** any **changes to remote versions** of the branches

```sh
  git branch <branchname> -m <newname>
```

### Only clone an specified branch from a remote repo

To fetch a specific branch’s content. This command is useful to fetch the
required branch quickly

```sh
  git clone -b <branch name> --single-branch <remote>
```

This can also be achived with adding the [remote](./95us.md) and **only
fetching** the **specifyied branch**

```sh
  git init
  git remote add <remote-name> <url>
  git fetch <remote-name> <remote-name>/<branch>
  git checkout <remote-name>/<branch>
```

### Add a remote branch locally

When you fetch **remote branchs** to **start working on them**, you **first**
need to **create a local branch** that tracks them

```sh
  git checkout <remote-name>/<branch>
  git checkout -b <branch>
  git remote -u <remote-name>/<branch> <branch>
```

A **faster way** can be achived with the `checkout` command

```sh
  git fetch --all
  git checkout -b <branch> <remote-name>/<branch>
```
