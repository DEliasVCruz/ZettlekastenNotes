# cli.git.flow.tool

Git-flow is a collection of extension that help you automate the operations of the
Vincent Driessen's branching model

## Overview

This tool provides a set of commands that automate the process of working with
[Vincent Driessen’s “git flow” branching model](./26yk.md), this **can be**
used at any point in your project and **dropped just as easily**.

It is just meant to **help** you **run** the task that compose **the workflow**

## Synopsis

```sh
  git flow <command> [flags]
```

## Commands

- init: Start a new git flow project
- feature: list, start or finish feature branches
- release: list, start or finish release branches
- hotfix: list, start or finish hotfix branches

## Options

- -d: accept all defaults

## Cookbook

### Work on a new feature branch

It will create a feature branch and **automatically switch to that branch**. It
will name the branch by appending the provided name to the default **feature
branch prefix**

By **default** it will **base** the new feature branch **from** the **current**
`HEAD` at the **develop** branch. The **base commit** should always come from
the `develop` branch

```sh
  git flow feature start <feature-name> [<base-commitbranch>]
```

After you've **finished working** run the `finish` command

```sh
  git flow feature finish [<feature-name>]
```

### Push feature branches to a remote

You can both `push` and `pull` feature branches from a remote repo

```sh
  git flow feature publish <name>
  git flow feature pull <remote> <name>
```

### Work with other supporting branches

You can use the same **subcommands** that you use with `feature` command to
work with `release` and `hotfix` branches

But what the `release` command won't do is **bump up the version number** this
you will have to **do manually**
