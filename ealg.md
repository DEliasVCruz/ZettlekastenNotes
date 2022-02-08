# lang.py.module.pdf.pypdf2.write

Create and write into PDF files

## Synopsis

```py
  from PyPDF2 import PdfFileWriter

  pdf_writer = PdfFileWriter()
```

## Overview

You can **create new** PDF files or write into existing ones. The
`PdfFileWriter()` class alone **can not create new content from scratch** other
than inserting new blank pages

## Cookbook

### Create and add pages to a new PDF file

You can create a new pdf file with the `PdfFileWriter()` class, this creates a
**new empty pdf** file with no pages.

```py
  from PyPDF2 import PdfFileWriter

  pdf_writer = PdfFileWriter()
```

### Add a blank page

To create new pages you would have to **add pages manually** with the
`.addBlankPage()` method. It **returns** a page object and can accept some of
the following **parameters**:

- `width`: The width of the new page in **points (1/72 of an inch)**
- `height`: The height of the new page in points

```py
  pdf_writer.addBlankPage(width=72, height=72)
```

### Add a page based on a page object

You can add pages to your PDF file with the `.addPage()` method. It
**requires** an **existing page object** as it's parameter

```py
  pdf = PdfFileReader('my_file.pdf')
  copied_page = pdf.getPage(2)              # Select the thrid page

  new_pdf = PdfFileWriter()
  new_pdf.addPage(copied_page)              # Add the copied page

  with open('new_pdf.pdf', 'wb') as output_file:
      output_file.write(new_pdf)
```

### Write the contents to a file

To write the contents to a file you need to **pass** a [file object](./7i8g.md)
opened **in binary write mode** to the `.write()` method of the `PdfFileWriter()`
instance

```py
  with open('file.pdf', mode='wb') as pdf_file:
      pdf_writer.write(pdf_file)
```

### Copy every page from a PDF file into a new one

You can copy every page from a `PdfFileReader()` instance to an instance of the
`PdfFileWriter()` class with the `.appendPagesFromReader()` method

```py
  pdf_reader = PdfFileReader('my_pdf.pdf')
  pdf_writer = PdfFileWriter()

  pdf_writer.appendPagesFromReader(pdf_reader)
```
