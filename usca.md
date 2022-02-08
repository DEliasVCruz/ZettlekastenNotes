# lang.py.module.pdf.pypdf2.manipulate

Rotate and crop pdf file pages

## Synopsis

```py
  from PyPDF2 import PdfFileReader, PdfFileWriter

  pdf = PdfFileReader('file.pdf')
  page = pdf.getPage(<index>)

  page.rotate[Counter]ClokWise()
```

## Overview

You can manipulate a page object by changing its orientation by **rotating it or
cropping it**

## Cookbook

### Rotate a page counter or clokwise

You can rotate a page `n` degrees left or right with the `.rotateClockWise()` and
`.rotateCounterClockWise` methods of the page object

```py
  first_page = pdf.getPage(0)
  rotated_page = first_page.rotateClockWise(90)     # Rotate the first page 90 degrees
```

### Find out if a page is rotated

Every page object has a `'/Rotate` key value that indicates the `n` degrees
that the page has been rotated

A `0` value **usually indicates** that a page has **not** been **rotated**.
However it **may** be the case that the page do **not have this key** or that
it will still be rotated even with a `0` value

```py
  for page, page_number in enumarate(pdf.pages):

      pages_to_revise = []

      try:
          page_rotation = page['/Rotate']
      except KeyError:
          pages_to_revise.append(page_number)
      else:
          if page_rotation != 0:
              page.rotateClockWise(-page_rotation)
      finally:
          modified_pdf.addPage(page)
```

### Crop parts of a page

Every page object has a `mediaBox` attributes that **returns** a
[list](./7cxo.md) with the cordinates of the lower left and upper right
cordinates that **represents** a **rectangular** area **defining** the
**boundaries of the page**

You can get **access** to each **individual corner cordinates** as
[tuples](./hsr4.md) with:

- `loweLeft`
- `lowerRight`
- `upperLeft`
- `upperRight`

By **modifiying** this **cordinate attributes** you can get a **cropped
version** of the page

When you change a corners cordinate the **other corners cordinates** get change
automatically **accordingly if so need** to preserve the rectangular shape

```py
  pdf = PdfFileReader('file.pdf')
  page = pdf.getPage(0)

  page.mediaBox.upperRighti                 # (792, 612)
  page.mediaBox.upperLeft                   # (0, 612)
  page.mediaBox.upperLeft = (0, 480)

  page.mediaBox.upperRighti                 # (792, 480)
  page.mediaBox.upperLeft                   # (0, 480)

  pdf_writter.addPage(page)
```
