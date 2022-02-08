# lang.py.module.pdf.camelot

A specialized library for table extraction on PDF files

## Synopsis

```py
  import camelot

  tables = camelot.read_pdf('file.pdf')
```

## Overview

This is an specialized module for **extracting tabular information** from tabular
data in `PDF` files

There are two main extraction strategies:

- `stream`: For tables that have whitespaces to simulate a table structure

  - Build upon [pdfminer](./fwzt.md) functionalities

- `lattice`: For tables with demarcated lines between cells

  - **Default strategy** when opening a file
  - Automatically parses multiple tables on a page

## Cookbook

### Open and extract tables from a pdf file

You can open and extract the tables of a pdf file with the `read_pdf()`
function. Thiw will **return** a [list](./7cxo.md) of **table objects** that
can be accessed by their index number

- You can **read encrypted files** with the `password=` parameter
- You can use the `stream` strategy with the `flavor='stream'` parameter

```py
  tables = camelot.read_pdf('my.pdf')
  print(tables)                             # <TableList n=2>
  print(tables[0])                          # <Table shape=(7, 7)>
```

### Remove unwanted characters from text

Sometimes text in your **table may include unwanted** characters such as spaces,
dots or newlines.

You can **get rid of them** with the `strip_text=` parameter that **accepts a string**
of **characters** to be removed

```py
# Get rid fo spaces, dots and new line characters
  tables = camelot.read_pdf('file.pdf', strip_text=' .\n')
```

### Select page numbers to extract from

By **default** it will **extract** tables **only from the first page** of the
document. You can specify what pages to extract tables from with the `pages=`
argument

- It takes pages as **comma-separated** [string](./4t3v.md) of page numbers
- It also takes care of rotated PDF pages automatically

```py
  tables = camelot.read_pdf('my.pdf', pages='1,2,3')    # Read pages 1, 2 and 3
  tables = camelot.read_pdf('my.pdf', pages='1-3')      # Read pages 1 to 3
  tables = camelot.read_pdf('my.pdf', pages='1,4-7')    # Read pages 1 and 4 to 7
  tables = camelot.read_pdf('my.pdf', pages='3-end')    # Read pages 3 to the end
  tables = camelot.read_pdf('my.pdf', pages='all')      # Read all the pages
```

### Display the contents of a table

By default `camelot` will save all the extracted tables as [panda's](./czyt.md)
dataframe objects

To display a table as a dataframe just call it's `.df` attribute

```py
  tables[0].df              # Display first table as a dataframe
```

### Export a table into different formats

You can export any table into **5 different formats** with the following
methods:

- `to_csv()`: Export table into a [csv](./rlaw.md) file
- `to_json()`: Export table into a [json](./evtw.md) file
- `to_excel()`: Export table into an [excel](./jbpc.md) file
- `to_html()`: Export table into an html file
- `to_markdown()`: Export table into a markdown file

```py
  tables[0].to_csv('file.csv')
```

### Get a report of the parsing results

To check how successful the parsing of the tables was you can use the
`.parsing_report` attribute of a table object

This will give you a [dictionary](./0loj.md) with **information about**:

- `accuracy`: The mmore the better
- `whitespace`: The less the better

```py
  tables[0].parsing_report

# {
    'accuracy': 99.02,
    'whitespace': 12.24,
    'order': 1,
    'page': 1
  }
```
