# cli.tar

Tar allow us to archive files into the `.tar` or `.tgz` format.

## Overview

This **only works with tar** files, check [zip](./kg1a.md) for zip files.

The `.tgz` format is a **compressed** version of the archive file through
**gzip**

## Synopsis

```sh
  tar [bundle-flags] <tarname> [<files2archive>]
```

## Options

- -c: create new archive
- -v: verbose
- -f: specify filename
- -x: extract file
- -z: file archve through gzip

## How to

### Create tar/tgz

```sh
  tar -czvf archive.tgz source_file
```

### Open or unzip or untar a tar/tgz

```sh
  tar -xvf unziped.tar
```
