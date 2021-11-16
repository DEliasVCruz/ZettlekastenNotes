# cli.zip

Use zip to unzip archived files under this extension, that is mainly for
windows programs

## Overview

This **only works with zip** files, check [tar](./m4jp.md) for tar files

## Synopsis

```sh
  zip [options] <zip-file> [<files2zip>]
  unzip [options] <zip-file> [options] [<target-directory]
```

## Options

### Zip command

- -q: quiet, hide the output from zip as it runs
- -r: include directories
- [0-9]: compression level (higher = longer)
- -e: encryption (provide a password)
- -l: list the files inside the zip

### Unzip command

- -q: quiet, hide the output from zip as it runs
- -d: provide a target directory
- -x: exclude files form being extracted

## Cookbook

### Create a compressed zip file

Here we create a zip file that includes files and directories; for **modertely
sized** zip files a **default compression of 6 is enough**. Here we are going
to provide higher compression

```sh
  zip -8 -rq zipename dir1/ *.py *.html
```

### Extracting files to a target directory

You can provide a target directory where to unzip the uncompressed files

```sh
  unzip -q zipedfile.zip -d ./targetdirectory
```

### List files insid a zip folder

```sh
  unzip -l zipfile.zip | bat
```

### Exclude files from being extracted

```sh
  unzip -q zipfile.zip -x <excluded-files>
```
