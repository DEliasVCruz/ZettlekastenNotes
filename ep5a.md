# cli.hardware.lspci

List pci devices in your system

## Synopsis

```sh
  lspci
```

## Overview

You can use the `lspci` command to list all the `pci` devices in your system, like:

- Audio card devices
- Network devices
  - Ethernet
  - Wifi
- USB controller
- Memory controller

## Cookbook

### List your audio devices

The `lspci` command prints a list of all devices, you can use [rg]() to filter
that list

```sh
  lspci | rg -i audio
```
