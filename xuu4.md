# lang.py.module.pdf.pypdf2.encryption

Encrypt and decrypt files with passwords

## Synopsis

```py
  pdf_writer.encrypt(<password>, <user>)
  pdf_reader.decrypt(<password>)
```

## Overview

You can set encryption of a PDF file and decrypt already encrypted files

## Cookbook

### Encrypt a PDF file

You can encrypt a file with the `.encrypt()` method of the `PdfFileWriter()`
class.

```py
  pdf_writer = PdfFileWriter('file.pdf')
  pdf_writer.encrypt(user_pwd='my_secret', owner_pwd='danielv')

  with open('encrypted_file.pdf', 'wb') as output_file:
      pdf_writer.write(output_file)
```

### Find if a PDF file is encrypted

You can find out if a pdf file is encrypted with the `.isEncrypted()` method of
the `PdfFileReader()` class

```py
  encrypted_pdf = PdfFileReader('encrypted.pdf')
  pdf = PdfFileReader('normal.pdf')

  encrypted_pdf.isEncrypted()               # True
  pdf.isEncrypted()                         # False
```

### Decrypt a PDF file

And you can decrypt a file with the `.decrypt()` method of the
`PdfFileReader()` class

```py
  pdf = PdfFileReader('encrypted_file.pdf')
  pdf.decrypt(password='my_secret')
```
