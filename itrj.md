# lang.py.module.pytest

The best Python testing module

## Synopsis

```py
  [import pytest]

  def test_<feature>():
      assert <assertion>
```

## Overview

Pytest is a framework for [testing code](../e051.md) in `Python` with a simple
structure and less boiler plate than in the common [alternative](./lrbi.md)

## Cookbook

### Create a test suit

With `pytest` creating a suit of tests is as esasy as **defining a function** and
using the `assert` [statement](./4g9v.md)

```py
  def test_uppercase():
      assert "loud noises".upper() == "LOUD NOISES"

  def test_reversed():
      assert list(reversed([1, 2, 3, 4])) == [4, 3, 2, 1]
```

### Test expected failure

If you want to **test** that you feature **throws** an **exception/error when**
you **use** a **bad value** or other similar situation. You can **use** the
`pytest.raises()` method **inside** a [context manager](./1rwn.md) to **safetly
handle** the raised exception and pass is such exception is raised and fail if
not

```py
  import pytest

  def f():
      raise SystemExit(1)

  def test_mytest():
      with pytest.raises(SystemExit):
          result = f()
```

You could also achive something similar with the `@pytests.mark.xfail` mark

```py
  @pytest.mark.xfail(raises=IndexError)
  def test_f():
      f()
```

- Using `pytest.raises()` is **better for**:

  - Testing **exceptions** your code is **deliberately raising**

- Using `@pytest.mark.xfail` **better for**:

  - Documenting **what "should" happen** in case of unfixed bugs

### Group multiple test in a class

You can group your tests inside classes for:

- Test organization
- Sharing fixtures for tests only in that particular class
- Applying marks at the class level and having them implicitly apply to all tests

```py
  class TestClassDemoInstance:
      value = 0

      def test_one(self):
          self.value = 1
          assert self.value == 1

      def test_two(self):
          assert self.value == 1
```

### Creating fixtures

In `pytest` fixtures are [functions](./8xrz.md) that **create data** or **test
doubles** or **initialize** some **system state** for the test suite

To create a fixture **return** it **as part of** a **function** and **decorate
it** with `pytest.fixture` [decorator](./ff01.md)

```py
  import pytest

  @pytest.fixture
  def example_people_data():
      return [
          {
              "given_name": "Alfonsa",
              "family_name": "Ruiz",
              "title": "Senior Software Engineer",
          },
      ]
```

For a **test** to accept **fixture** it must **accept** it **as an argument**

```py
  def test_format_data_for_display(example_people_data):

      output = format_data_for_display(example_people_data)
      expected_result = "Alfonsa Ruiz: Senior Software Engineer"

      assert output == expected_result
```

### Create fixture that are used automatically (`autouse`)

You can create fixtures that will be **used by all tested automatically** even if
they are **not explecitly called** as dependencies with the `autouse=True` argument

```py
  @pytest.fixture
  def first_entry():
      return "a"

  @pytest.fixture
  def order(first_entry):
      return []

  @pytest.fixture(autouse=True)
  def append_first(order, first_entry):
      return order.append(first_entry)

  def test_string_only(order, first_entry):
      assert order == [first_entry]
```

### Define the scope of a fixture

Fixtures are created when first requested by a test, and are **destroyed based on
their scope**

You can use this to create fixtures that will only be re-run based on their
scope, otherwise their **scope** will be **captured and maintained**

- `function`: Destroyed at the end of a test (**default**)
- `class`: Destroyed during teardown of the last test in the class
- `module`: Destroyed during teardown of the last test in the module
- `package`: Destroyed during teardown of the last test in the package

**In this example** the `SMTP` connection won't we be made more than once for every
test in the module

```py
  @pytest.fixture(scope="module")
  def smtp_connection():
      return smtplib.SMTP("smtp.gmail.com", 587, timeout=5)
```

### Clening up after a fixture

If your fixture initiates some state in your testing environment that need to
then be reverted once the testing has ended, like creating and deliting users,
you can use the [yield](./4g9v.md) and everythin after will be run once testing has
ended

```py
  @pytest.fixture
  def sending_user(mail_admin):
      user = mail_admin.create_user()
      yield user
      mail_admin.delete_user(user)
```

### Scaling fixtures (`conftest.py`)

If you find yourself using a fixture repeatedly throughout your project you
could move them to more general fixture-related modules

You can setup your fixtures in a file called `conftest.py`. Pytest **will look
for** this files in your directory tree and they will be **available for use**
in the **paraent directory** it's found and it's **subdirectories**

### Guard access to resources

You can also use fixtures to **avoid real connections and resources to be
used** by your test. So you can **use** a `monkeypatch` fixture to **replace
values and behavior**

To do so you need to place this fixtures in a `conftest.py` and pass the
`autouse=True` parameter to the `pytest.fixture()` decorator

**In this example** we are ensuring that network calls will be disabled in every
test across the suite.

```py
# conftest.py

import pytest
import requests

@pytest.fixture(autouse=True)
def disable_network_calls(monkeypatch):
    def stunted_get():
        raise RuntimeError("Network access not allowed during testing!")
    monkeypatch.setattr(requests, "get", lambda *args, **kwargs: stunted_get())
```

### Categorize tests (`marks`)

You can categories for your tests and provides options for including or
excluding categories when [running your suite](./b42q.md)

- You can mark a test with any number of categories
- Is usefull for categorizing tests by subsystem or dependencies.
- To **create a mark** you use the decorator `@pytest.mark.<my-mark-name>`

**In this example** we mark a test that requires access to a database

```py
  @pytest.mark.database_access
  def test_update_database():
      ...
```

Pytests provides a few **built-in marks**:

- `skip`: Skips a test unconditionally
- `skipif`: skips a test if the expression passed to it **evaluates** to `True`
- `xfail`: Indicates that the **test** is **expected** to **fail**
- `parametrize`: Creates multiple variants of a test with different values as arguments

### Use marks on a class or module level

You can put marks on your:

- **Tests classes**: Like **applying** the marker to **every method** in the class

```py
  import pytest

  @pytest.mark.webtest
  class TestClass:
      def test_startup(self):
          pass

      def test_startup_and_more(self):
          pass
```

- **Module level**: Applies for every class and function in the module

```py
  import pytest
  pytestmark = [pytest.mark.webtest, pytest.mark.slowtest]
```

### Parametrize your test

- Use parametrization to **separate** the test **data from** the test **behavior**
- Use it pass different inputs to the same test and evaluate results
- To create it you decorate test with the `@pytest.mark.parametrize()` mark.

This will **accept** a [string](./4t3v.md) with **variables separated by
comas**, or a tuple, and a [list](./7cxo.md) with either **single values or**
[tuples](./hsr4.md) with values **corresponding** to each **variable**

```py
  @pytest.mark.parametrize("maybe_palindrome,expected_result", [
      ("", True),
      ("a", True),
      ("Bob", True),
      ("Never odd or even", True),
      ("Do geese see God?", True),
      ("abc", False),
      ("abab", False),
  ])
  def test_is_palindrome(maybe_palindrome, expected_result):
      assert is_palindrome(maybe_palindrome) == expected_result
```

### Mark indivual parametrize inputs

You can apply **marks** to a **whole parametrize** test and **also** apply it
to **indivual parametrize** inputs with `pytests.param(*args, marks=<mark>)`

```py
  import pytest

  @pytest.mark.foo
  @pytest.mark.parametrize(
      ("n", "expected"),
      [(1, 2), pytest.param(1, 3, marks=pytest.mark.xfail), (2, 3)]
  )
  def test_increment(n, expected):
      assert n + 1 == expected
```
