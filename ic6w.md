# cli.tools.core.compression.gzip

A compression format for the web

## Synopsis

```sh
  gzip [options] <file>
```

## Overview

You can compress files losslessly with gzip and is more wildly used to compress
files to run throught a network, most commonly when serving files from the web

- It can only compressed individual files, it can't compress an entire directory

## Options

- `-l`: Show information about a compressed file
- `-d`: Decompress a gziped file

## Cookbook

### Compress a single file

You can compress a single file just by passing it as an argument to the `gzip`
command

```sh
  gzip <file-name>
```

### Get information about the compress file

You can use the `-l` flag to print information about a gziped filed such as:
  - **The compress ratio**: The higher it is the more space that was saved

```sh
  gzip -l <gzip-file.gz>
```

### Decompress a file

You can use the `-d` flag to uncompressed a gziped file into it's original
form or you can use the shortcut `gunzip` command

```sh
  gzip -d <gzip-file.gz>
  gunzip <gzip-file-2.gz>
```

### Compress multiple files

On it's own `gzip` can't compress an entire directory. For that you'll first
need to use an archiver like [tar](./m4jp.md)

- Use the `tar` command with the `-z` flag to compress multiple files

```sh
  tar -czvf <tgz-file.tar.gz> [<source-files>|<directory>]
```
