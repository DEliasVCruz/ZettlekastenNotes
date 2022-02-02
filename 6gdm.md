# lang.py.module.openpyxl.images

Insert images into your workbook file

## Synopsis

```py
  from openpyxl.drawing.image import Image

  image = Image('my_image.png')
  sheet.add_image(image, <cell>)
```

## Overview

To manipulate images you wil first have to instal the `pillow` library. And
then you can use the `Image()` class to create an image object that you can
manipulate and insert in your [workbook](./kz9z.md) file

## Cookbook

### Add an image to your file

You can add an image by **creating and instance of** the `Image()` class with
the given image

You can then **insert** the image **with** the `add_image()` method of the
[sheet](./tmox.md) object

- The **first argument** takes the instance of the `Image()` class
- The **second argument** takes a top left anchor [cell](./n3z1.md) for the image
  to be inserted at

```py
  from openpyxl.drawing.image import Image

  logo = Image("logo.png")
  sheet.add_image(logo, "A3")
```

### Change the height and width of the image

You can modifify the `height` and `width` attribute to change those values of
the image

```py
  logo = Image("logo.png")

  logo.height = 150
  logo.width = 150
  sheet.add_image(logo, "A3")
```
