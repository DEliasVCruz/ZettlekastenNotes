# cli.py.poetry

An environment and dependencies management tool for Python

## Synopsis

```sh
  poetry [comands]
```

## Overview

A virtual **environment management tool** and **dependency manager** for your `Python`
applications. It can also help you **setting your project structure** and
**requirements** as well as it's **deployment** to `PyPi` or other hosting platforms

## Cookbook

### Install poetry

It is best to install poetry system wide instead of with [pip](./eioz.md)
since it can generate conflicts. Therefore use this install script or visit the
official [install page](https://python-poetry.org/docs/#installation)

```sh
  curl https://raw.githubusercontent.com/python-poetry/poetry/master/install-poetry.py
  | python3 -
```

You can **update poetry** with:

```sh
  poetry self update
```

### Create a new project

You can create a new project **with** the `new` command

```sh
  poetry new rp-poetry
```

This will **create** a new folder with the given project name and a **basic
directory structure** inside it.

```sh
  rp-poetry/
  │
  ├── rp_poetry/
  │   └── __init__.py
  │
  ├── tests/
  │   ├── __init__.py
  │   └── test_rp_poetry.py
  │
  ├── README.rst
  └── pyproject.toml
```

You can also use the `--src` flag to give a **src** structure to your **project**

```sh
  poetry new --src rp-poetry
```

It will output the **following structure**:

```sh
  rp-poetry/
  │
  ├── src/
  │   │
  │   └── rp_poetry/
  │       └── __init__.py
  ....
```

By default it will create an initial package with a normalize version of the
project name, you can adjust it with the `--name` flag

```sh
  poetry new rp-poetry --name realpoetry
```

### Configure your project

You can add configuration for different tools in your project **with** the
`pyproject.toml` file. In there the **tools** are **defined by** `tool.<tool-parts>`
**syntax** as the **sub table name**

Under the `tool.poetry` sub table there are for mandatory keys:

- **name**: The name of your **package**
- **version**: The version of your package using **semantic versioning**
- **description**: A **short** description of your package
- **authors**: A list of authors, in the format `name <email>`

```toml
  [tool.poetry]
  name = "rp-poetry"
  version = "0.1.0"
  description = ""
  authors = ["Philipp <philipp@realpython.com>"]

  [tool.poetry.dependencies]
  python = "^3.9"

  [tool.poetry.dev-dependencies]
  pytest = "^5.2"

  [build-system]
  requires = ["poetry-core>=1.0.0"]
  build-backend = "poetry.core.masonry.api"
```

### Working with virtual environments

By **default** `Poetry` **creates** the virtual environments **in** the
`~/.cache/pypoetry` folder

You can **check** if your **virtual environment** is **activated** with `env
list` command that will **return no output** if the virtual environment **is not
activated**

```sh
  poetry env list
```

### Install dependencies

You can use the `install` command that will **check** your `pyproject.toml`
file **for specified dependencies** then resolves and installs them

You should **only install** dependencies **this way** if there is **no**
`poetry.lock` file **present**, doing so after manually changing the
dependencies on the `pyproject.toml` file will cause an error

```sh
  poetry install
```

It also **install the project itself**, that way you can **import** it
**anywhere right away**

```py
  from rp_poetry import __version__

  def test_version():
      assert __version__ == "0.1.0
```

### Add new packages ass dependencies

You can **add new external packages** as dependencies with the `add` command this
will **installed** them with the **latest compatible version** of this package.

And it will **automatically add them to** your `pyproject.toml` and pin them on the
`poetry.lock` file

```sh
  poetry add requests
```

To add a **developer only** dependency you can **use** the `--dev` flag

```sh
  poetry add black --dev
```

### Update dependencies after defining the manually

If you have **manually defined** your **dependencies** in the `pyproject.toml`
file, then to have them **updated (but not installed)** in your **project** you need
to **use** the `lock` command to pin them on the `poetry.lock` file

```sh
  poetry lock
```

If you **only** want it to **update** the **new dependencies** and **keep** the
**already set** dependencies **intact** you can **use** the `--no-update` flag

```sh
  poetry lock --no--update
```

### Update dependencies based on project constrains

You can also **update dependencies based on** your `pyproject.toml` **specified
version constrains** with the `update` command. This will **update, lock and
install** them

You can **update only specified packages** by defining them in your command

```sh
  poetry update [<packages>]
```

If you wan to update them with **versions outside** of your **version
constrains** you need to **use** the `add` command and pass the **specified
package** with **either** an specific **version number or** the `@latest`.
After that you **must run** `install` to **lock** them **and install** them

```sh
  poetry add pytest@latest --dev
  poetry install
```

You can use the `--dry-run` flag to **display** the **operations** in your
terminal **without executing** any of them. It **works both for** `add` and
`update` that way you can decide wich is better

```sh
  poetry add --dry-run pytest@latest --dev
  poetry update --dry-run pytest
```

### Install dependencies after updating lock file

After you have updated your `poetry.lock` file to be in sync with your `pyproject.toml`
to be able to use them in your environment you have to installed them with the
`install` command

```sh
  poetry install
```

Before this would have raised an error since the `pyproject.toml` and
`poetry.lock` file would have been out of sync

### Use poetry with an existing project

Regardless of the structure of your project you can use `init` command to **start
using** `Poetry` with your **existing project**

```sh
  poetry init
```

### Execute python commands

You can execute python commands like [pytest]() with the `run` command. This
will **execute** them **using** your **virtual environment version** of those commands

```sh
  poetry run pytest
  poetry run python <cript>
```

### Create a REPL of your virtual environment

You can **create** a `REPL` of your **current virtual environment** by **using**
the `run` command and passing `python`

```sh
  poetry run python
```

### Get info about your installed packages

Much like [pip](./eioz.md) you can **get info** about your **installed
packages** with the `show` command.

```sh
  poetry show [<package>]
```

Additionally you can use the `--tree` flag to **list all dependencies as a tree**

```sh
  poetry show --tree
```

### Import and use an existing requirements.txt file

You can use an existing `requirements.txt` file by `cat` it to the `add`
command

```sh
  poetry add `cat requirements.txt`
```

### Export to a requirements.txt file

If for some reason you need a `requirements.txt` version of your dependencies
you can **use** the `export` command

```sh
  poetry export --output requirements.txt
```
