# lang.rst.syntax.intra_links

You can provide **cross-referential links** within the same or related documents in
your proyect. **You will need** `Sphinx` for this functionality

## Synopsis

```rst
  .. _reference_name:
  :ref:`reference_name`
```

## Cookbook

### Reference an specific section of another file

Provided you have 2 documents (`installation.rst` and `index.rst`)

On `installation.rst` write:

```rst
  .. _install-guide:

  Installation Guide
  ==================

  1. Create and activate a virtual env
  2. ``pip install`` it
```

And on `index.rst` yow would reference it by:

```rst
  For details on how to install, please
  read :ref:`install-guide`.
```
