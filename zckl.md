# info.py.project_structure

How to structure your Python project

## Overview

- Your project **should** generally **consist** of **one top-level** [package](./2oy5.md)
  usually **containing sub-packages**.

- That top-level package usually **shares the name** of your **project**, and
  exists **as** a **directory in** the **root** of your project's repository.

- This top-level package **can also be contained inside** a `src` directory

## Cookbook

### Project structure for a simple project

If you are creating a throw away **application** that may **consist of a single script**

```sh
  helloworld/
  │
  ├── .gitignore
  ├── helloworld.py
  ├── LICENSE
  ├── README.md
  ├── requirements.txt
  ├── setup.py
  └── tests.py
```

### Create an application with internal packages

When creating a more complex application it is best to separate different
components of your app into their own directories

- `<mypackage>`: Here you will have your main application code

  - `__main__.py`: This will make your project [executable](.2oy5.md)
  - `__main__.py`: Indicates that the directory is a package
  - `[runner/app].py`: A module that will serve as the entry point
  - Every other sub package should have it's own `__init__.py` module

- `data`: It’s a central location for any files that your application will
  ingest or produce

  - Is helpfull for testing
  - Your [fixtures](./e051.md) can live here

- `docs`: A place to store your application docs

  - They can be manually written or auto-generated
  - Should have one per module

- `test`: A place to store all your tests

  - They should be sparated based on your packages and modules
  - They don't need a `__init__.py` module

- `bin`: Should contain any executable files

```sh
  helloworld/
  │
  ├── bin/
  │
  ├── docs/
  │   ├── hello.md
  │   └── world.md
  │
  ├── helloworld/
  │   ├── __init__.py
  │   ├── runner.py
  │   ├── hello/
  │   │   ├── __init__.py
  │   │   ├── hello.py
  │   │   └── helpers.py
  │   │
  │   └── world/
  │       ├── __init__.py
  │       ├── helpers.py
  │       └── world.py
  │
  ├── data/
  │   ├── input.csv
  │   └── output.xlsx
  │
  ├── tests/
  │   ├── hello
  │   │   ├── helpers_tests.py
  │   │   └── hello_tests.py
  │   │
  │   └── world/
  │       ├── helpers_tests.py
  │       └── world_tests.py
  │
  ├── .gitignore
  ├── LICENSE
  └── README.md
```
