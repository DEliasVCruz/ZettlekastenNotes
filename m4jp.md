# cli.tar

Tar allow us to archive files into the `.tar` or `.tgz` format.

## Overview

The `tar` command takes multiple files and combines them into a single file
which is known as a **tarball**

- This **only works with tar** files, check [zip](./kg1a.md) for zip files.
- The `.tgz` format is a **compressed** version of the archive file through [gzip](./ic6w.md)

## Synopsis

```sh
  tar [bundle-flags] <tarname> [<files2archive>]
```

## Options

- `-c`: create new archive
- `-C`: Specify a directory for extraction
- `-v`: verbose
- `-f`: specify filename
- `-x`: extract file
- `-z`: compress the tarball with gzip

## Cookbook

### Create tar/tgz

```sh
  tar -czvf archive.tgz source_file
```

### Open or untar a tar/tgz

```sh
  tar -xvf unziped.tar
```

### Extract the contents into a target directory

You can untar the contents of a file into a different directory than the
one you are currently on with the `-C` option

```sh
  tar -xvf tar_file.tar[.gz] -C /path/to/dir
```
