# lang.py.syntax.loggin

Python's native log keeping capabilities with the standard logging library

## Synopsis

```py
  import logging
```

## Overview

The logging module provides with a **basic logger** to log messages and can be used
**without much configuration** and gives it the **default name** of **root**

There are **5 default log levels** depending on the degree of severity;

- **DEBUG**: Called with `logging.debug('This is a debug message')`
- **INFO**: Called with `logging.info('This is an info message')`
- **WARNING**: Called with `logging.warning('This is a warning message')`
- **ERROR**: Called with `logging.error('This is an error message')`
- **CRITICAL**: Called with `logging.critical('This is a critical message')`

## Cookbook

### Basic logger configuration

You can config your logger with the `basicConfig()` function, and **it can only
be called once** further call will not have any effect

Some of it's commonly used parameters are:

- `level`: It will **only log** messages from the **specified severity and above**
- `filename`: A **file where to write** the **logs** to instead of to the console
- `filemode`: What mode to [open](./7i8g.md) the file at. Default is `a` for **append**
- `format`: **Format** of the **log message**

You can find **more configuration parameters** [here](https://docs.python.org/3/library/logging.html#logging.basicConfig)

```py
  import logging

  logging.basicConfig(
      level='logging.WARNIGN'
      filename='app.log',
      filemode='w',
      format='%(name)s - %(levelname)s - %(message)s'
  )
  logging.warning('This will get logged to a file')

  # root - ERROR - This will get logged to a file
```

### Formatting the output

Trough the `format` argument you can **customize the output** of your
**logger** with the use of **placeholder variables** like:

- `%(asctime)s`: Add date and time info. **Can be configured** with `datefmt` argument
- `$(message)s`: The **logged message**
- `%(levelname)s`: The **logging level**
- `%(process)d`: The **process id**
- `%(name)s`: The **name of the logger**

A full list of **place holder variable** can be found [here](https://docs.python.org/3/library/logging.html#logrecord-attributes)

```py
  import logging

  logging.basicConfig(format='%(asctime)s - %(message)s', level=logging.INFO)
  logging.info('Admin logged in')

  # 2018-07-11 20:12:06,288 - Admin logged in
```

### Add dinamic data to your log message

You can use `f-strings` in your logg message you add variable data to the output

```py
  import logging

  name = 'John'
  logging.error(f'{name} raised an error')

  # ERROR:root:John raised an error
```

### Add trace error info

When you hit an **excpetion** [error](./t7gf.md) you can capture the traceback
info in your log message by two ways

- Passing the `exc_info=True` parameter to your logger call
- Using the `logging.exception()`:
  - This logs an error level message and adds teh exception
  - It should always only be used inside an [exception](./wvgx.md) handler

```py
  import logging

  a = 5
  b = 0

  try:
    c = a / b
  except Exception as e:
    logging.exception("Exception occurred")
  except Exception as e2:
    logging.error("Exception occurred", exc_info=True)
```

### Creating your own logger object

If you are going to perform logging across multiple [modules](./2oy5.md) in a big
application is **best practice** to **instantiate** your own **custom logger**
[class](./unhs.md) for the specified needs

You can **do this with** the `logging.getLogger()` class instantiator. It is
**best practice** to **name the logger with** the `__name__` magic attribute.
To keep track to what module it is logging from.

```py
  import logging

  logger = logging.getLogger(__name__)
  logger.warning('This is a warning')
```

### Customizing an instantiated logger object

You **can't customize** the **custom logger** with the `logger.basicConfig()`
function.

For that you **need to use**

- `Handlers`: The **send** the logged messages **to configured destinations**

  - Such as:

    - The **console** (`logging.StreamHandler()`)
    - A **file** (`logging.FileHandler()`)
    - Over **HTTP** (`logging.HTTPHandler()`)
    - To an **email** via SMTP (`logging.SMTPHandler()`)

  - A created logger **can have more than one handler**
  - You can set **different severity levels for** each **handler**

- `Formatters`: With this you can **format the output** of your custom logger

```py
  import logging

# Create a custom logger
  logger = logging.getLogger(__name__)

# Create handlers
  console_handler = logging.StreamHandler()
  file_handler = logging.FileHandler('file.log')
  console_handler.setLevel(logging.WARNING)
  file_handler.setLevel(logging.ERROR)

# Create formatters and add it to handlers
  console_format = logging.Formatter('%(name)s - %(levelname)s - %(message)s')
  file_format = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
  console_handler.setFormatter(console_format)
  file_handler.setFormatter(file_format)

# Add handlers to the logger
  logger.addHandler(console_handler)
  logger.addHandler(file_handler)

  logger.warning('This is a warning')
  logger.error('This is an error')
```
