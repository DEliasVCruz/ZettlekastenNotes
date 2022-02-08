# lang.py.module.pdf.pdfminer

Third party library for extracting text data from PDF files

## Synopsis

```py
  from pdfminer.high_level import <function-API>
```

## Overview

The `pdfminer.six` library provides a set **high level function** APIs that allow
you to do **common operation** for extracting information from PDF files

It is very **basic** in it's **scope** but **excellent** in its **usage** as an
**extraction tool** of **textual data** in your PDF file

For **more general** reading, creation and manipulation of PDF file see:

- [pypdf2](./4x1x.md): A general usage PDF file manipulation

## Cookbook

### Extract all the text from a PDF file

You can **extract** all the **selectable text** in a PDF file with the
`extract_text()` function

It **returns** the contents as a **single** [string](./4t3v.md) and accepts
some of the following **parameters**:

- `pdf_file`: A file path or [file like object](./bwao.md)
- `password`: Password for decryption
- `page_numbers`: [List](./7cxo.md) of `zero-index` page numbers to extract
- `maxpages`: Maximum number of pages to extract

```py
  from pdfminer.high_level import extract_text()

  text = extract_text('file.pdf')
```

### Extract pages from a PDF file

**Extract** and yield **page objects** from a PDF file with the `extract_pages()`
function. It accepts the same parameters as `extract_text()`

```py
  from pdfminer.high_level import extract_pages()

  # Extract pages 3, 4 and 6
  pages = extract_pages('file.pdf', page_numbers=[2,3,5])
```
