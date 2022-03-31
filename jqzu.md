# cli.stow

The GNU dotfiles manager

## Synopsis

```sh
  stow [options] <destination> <program>
```

## Overview

You can manage your dotfiles easily with this program. In **escence** is just a
[symbolic link](./55ut.md) **generator**

### Flags

It's more important **flags** are:

- `-v`: Show the actions with a verbose output
- `-R`: Clean old reference first before making new symlinks
- `-t`: Specifies the target directory

### Basic structure

The basic structure consists of directory names as programs names. And the
inside you design the structure as you would to get to those files from the
target directory

## Cookbook

### Creating a dotfile for a program

Assumming that the program uses an `xdg` desktop configuration practices. Then
it's dotfiles will be stored inside the `.config/` directory under the name of
the application

- To create a stow dotfile equivalent just **replicate that structure**

```sh
  mkdir -p kitty/.config/kitty
```

### Add a new configuration to a program

To **add a new dotfile** configuration to your system you can **run**

```sh
  stow -v -R -t ~ kitty
```

### Reference a configuration file from a separate git repo

You can use the [git submodules](./b5zh.md) command to reference a
configuration in a different git repo and it will be linkedd to

```py
  git submodule add <config-fepo> <config>/
```

### Automate your dotfiles managment

You can use this script to automate the installation of dotfiles on your system

```sh
#!/usr/bin/env bash

# make sure we have pulled in and updated any submodules
  git submodule init
  git submodule update

# what directories should be installable by all users including the root user
  base=(
      zsh
  )

# folders that should, or only need to be installed for a local user
  useronly=(
      git
  )

# run the stow command for the passed in directory ($2) in location $1
  stowit() {
      usr=$1
      app=$2
      # -v verbose
      # -R recursive
      # -t target
      stow -v -R -t ${usr} ${app}
  }

  echo ""
  echo "Stowing apps for user: ${whoami}"

# install apps available to local users and root
  for app in ${base[@]}; do
      stowit "${HOME}" $app
  done

# install only user space folders
  for app in ${useronly[@]}; do
      if [[! "$(whoami)" = *"root"*]]; then
          stowit "${HOME}" $app
      fi
  done

  echo ""
  echo "##### ALL DONE"
```
