# lang.py.module.pdf.pypdf2.read

Open and read PDF files

## Synopsis

```py
  from PyPDF2 import PdfFileReader

  pdf = PdfFileReader(<file>)
```

## Overview

Read and get **basic information and metadata** from a PDF file

- Some of the **methods** of the instance are:

  - `.getNumPages()`: The number of pages in the PDF
  - `.getPage()`: Select a page based on it's index number

- Some the **attributes** of the instance are:

  - `pages`: Returns an iterable of all the file page objects
  - `documentInfo`: Get the metadata at the PDF creation
    - It returns a [dictionary](./0loj.md)
    - The elements can be accessed as keys or as attributes

## Cookbook

### Open a PDF file

You can read a PDF file with the `PdfFileReader` class, it **can't accept** a [file
object](./bwao.md) so you would **have to convert** it to a string representation
of the file path

It also **takes care of** the **closing** of the **file** after is used

```py
  from PyPDF2 import PdfFileReader
  from pathlib import Path

  pdf_path = Path().home() / my_file
  pdf = PdfFileReader(str(pdf_path))
```

### Get basic info from a file

You can get basic information from a file like the **number of pages** or the
**creation metadata** with `.getNumPages()` and `.documentInfo` respectively

The `.documentInfo` you **can access** it's elements as **dictionary keys** or as
**attributes**

```py
  pdf.getNumPages()                         # 2

  metadata = pdf.documentInfo

  metadata['/Title']]                       # 'Mi Titulo'
  metadata.title                            # 'Mi Titulo'
```

### Get the page number of a page

You can get the page number of a page with the with the `.getPageNumber()`
method of the `PdfFileReader()` class

You have to pass a page object as it's parameter and it will return the `0
index` number of that page

```py
  for page in pdf.pages:
      if pdf.getPageNumber(page) == 5:      # Break if we are on page 6
          break
```

### Select a page from the PDF

You can select page from the PDF **as a page object** with the `getPage()` method.
Pages can be **referenced by** their `zero-index` **number**

```py
  first_page = pdf.getPage(0)               # First page as a page object
```

### Iterate over the pages of a PDF

You can [iterate](./p7q9.md) over the pages of a `Pdf` file with the `pages` attribute

```py
  for page in pdf.pages:
      print(page.extractText())
```

The `.pages` attribute also **supports slicing and indexing**

```py
  new_pdf = PdfFileWriter()

  for page in pdf.pages[1:4]:               # Select the second to fourth page objects
      new_pdf.addPage(page)
```

### Extract all the text from a page

You can use the `extractText()` method of a page object to extract all the text
it contains

The **results** are **usually suboptimal** and you'll be **better of** using [pdfminer](./fwzt.md)

```py
  first_page = pdf.getPage(0)
  text_data = first_page.extractText()
```
