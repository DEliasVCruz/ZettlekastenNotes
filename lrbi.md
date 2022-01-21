# lang.py.module.unittest

Python's standard library default testing module

## Synopsis

```py
  import unittest

  class Test<Feature>(unittest.TestCase):

      def test_<tested-functionality>(sef):
          self.assert<Assertion>(<assertion>, <ought-to-be-result>)

  if __name__ == '__main__':
      unittest.main()
```

## Overview

You can perform unit testing using some **basic assetions** with the **built
in** module `unittest`

### Assertion methods

It **comes with** some **basic assertions**:

- `asssertEqual(a, b)`: Assert that "a" is equal to "b" (`a == b`)
- `asssertTrue(x)`: Assert "x" is the [bool](./6auy.md) "True"  (`bool(x) is True`)
- `asssertFalse(x)`: Assert "x" is the bool "False"  (`bool(x) is False`)
- `asssertIs(a, b)`: Assert "a" is the **same object in memory** as "b" (`a is b`)
- `asssertIsNone(x)`: Assert "x" is equal to [None](./y624.md) (`x is None`)
- `asssertIn(a, b)`: Asset "a" is **included in** the object "b" (`a in b`)
- `asssertIsInstance(a, b)`: Assert "a" is instance of "b" (`isinstance(a, b)`)
- `asssertRaises(Exception)`: Assert that an [error](./t7gf.md) was **raised**

The **last argument in** our **assertion method** is the [string](./4t3v.md)
that will be printed in case the test fails. It **should contain** a
**message** of **what was the expected** value and **what you actually got**

## Cookbook

### Create a test for a feature

To create a test suite you need to **structure them as** [classes](./unhs.md) that
**inherit** from the `unittest.TestCase` class and **use** the
`assert<Asertion>()` methods

**In this example** we test our custom sum function [imported](./2oy5.md) from
a module called `my_sum` in the same directory as the test suite

```py
import unittest
from my_sum import sum

class TestSum(unittest.TestCase):

    def test_list_int(self):
        """
        Test that it can sum a list of integers
        """
        data = [1, 2, 3]
        result = sum(data)
        self.assertEqual(result, 6, "It should be 6")

if __name__ == '__main__':
    unittest.main()
```

### Test expected failures

If you want to **test** that you feature **throws** an **exception/error when**
you **use** a **bad value** or other similar situation. You can **use** the
`assertRaises()` method **inside** a [context manager](./1rwn.md) to **safetly
handle** the raised exception and pass is such exception is raised and fail if
not

```py
  import unittest
  from my_sum import sum

  class TestSum(unittest.TestCase):

      def test_bad_type(self):
          data = "banana"
          with self.assertRaises(TypeError):
              result = sum(data)
```

### Create a setup for your test

You can have a setup for your tests that **will be runned before the other
elements of your suit** test start running by creating a `setUP` method

```py
  import unittest

  class TestBasic(unittest.TestCase):

      def setUp(self):
          # Load test data
          self.app = App(database='fixtures/test_basic.json')

      def test_customer_count(self):
          self.assertEqual(len(self.app.customers), 100)
```
