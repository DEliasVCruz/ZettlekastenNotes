# lang.py.module.gui.tkinter

Built-in module for building crossplataform gui interfaces

## Synopsis

```py
  from tkinter import Tk
```

## Overview

You can use tkinter to write native looking cress plataform gui
interfaces to your python programs

- Is limited on it's options and configuration, as well as it having a fairly
  complitacated and convuluted API

But if you need to create a zero-dependecies and relatively simple
GUI, then using tkinter is an adequeate choice

## Cookbook

### Open a file or directory picker

You can ask the user for input on what files to open or save as with:

- `askopenfilename()`: Ask the to chose one file from it's filesystem
- `askopenfilenames()`: Ask the user to chose one or more files
  - Returns a single string or a [tuple](./hsr4.md) of strings
- `asksaveasfilename()`: Ask the user to chose a name or file to save as

All this options return a [string](./4t3v.md) representation of the full path
to the files selected or specified

- You can also ask for the user to select a directory with `askdirectory()`

```py
  from tkinter.filedialog import askopenfilenames, asksaveasfilename, askdirectory

  root = tk.Tk()
  root.withdraw()

  filenames = askopenfilenames(
                    tittle="El titutlo de la ventana",
                    filetypes=(("Archivos zip", "*.zip"), ("Todos", "*.*"))
                  )

  save_file = asksaveasfilename(
                    confirmoverwrite=True,
                    defaultextension="csv",
                    filetypes=(("Archivos CSV", "*.csv"), ("Todos los archivos", "*.*"))
                    title="Seleccione archivo a guardar"
                  )

  dir_name = askdirectory(
                    mustexist=True,
                    title="Selecciona una carpeta"
                  )
```
