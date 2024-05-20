# lang.py.syntax.classes

An object creation and instantiating structure

## Synopsis

```py
  class <Name>[(<Parent-Class>)]:

      [<class-variable> = <value>]

      def __init__(self, atr1, atr2):
          [<opearations>]
          self.atr1 = atr1
          self.atr2 = atr2

      [<other methods]
```

## Overview

The basic way of **Object Oriented Programming** in Python is through classes

### Inheritance

Some of the advantages of using class inheritance

- Allows us to **create parent and sub classes**
- **Inherit** attributes and methods
- **Get** all the **functionalities** of the **parent class**
- Add or overwrite completely **new functionality without affecting** the
  **parent class**

When a child class calls a method, it will do so by applying the **Method
Resolution Order**. In which Python will climb a chain of inheritance until it
finds the appropriate method that resolves the call

### Class vs Static method

**When** to most used a **static method**:

- A function that has some **logical conection** to your class **but** is **not dependant**
  on any specific **instance** of it

**When** to most used a **class method**:

- Provinding **alternative** ways **to instantiate instances** of your class. Usually
  some kind of structured data

In general is **not recommended** to call this method from the **instance level**

### Setters and Getters

- **Getter**:

  - In OOP in `Python` a **getter** is a **function** that **retrieves read
    only attributes** and is implemented **through** the `@property` decorator

- **Setter**:

  - And a **setter** is a way to enable changing the values of read only attributes
    (encapsulated) and is implemented through the `@<attribute-name>.setter`
    decorator

  - A **good use** for setters is to **restrict** what **values** can be assigned
    to an **attribute**. This is caled the **encapsulation principle**

You must take notice that are **in esence just functions** so you **could extra logic**
and operations to be **executed** whenever this special attributes are called

### Polyphormis

A **single entity can handle different version of an object accordingly**. So a
parent class method can handle instances of it's child method according to that
subclass characteristics

### Singletons

A singleton is a class with only one instance. There are some examples of
singletones in `Python` such as `None`, `True` and `False` this is what
allows you to compare against them with the `is` keyword since it returns
`True` for objects that are the exact same instance

## Cookbook

### Define a class instance attributes

When you define a class you need to **define** the [magic method](./a8n3.md)
`__init__` that takes the **object** it **self as** it's **first parameter**.
This will **execute every time** you **create** a **new instance** of the class

You **can operate** on the passed **values** as much **as you want** before
passing them as attributes or not passed them at all

```py
 class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = f"{first}.{last}@email.com"
```

### Define a class instance method

You can define **methods like** if they were **regular**
[functions](./8xrz.md). But their **first argument must be** the instance
itself with `self`

It's **best if** this methods are **related to** the **attributes** of the
instance itself. Otherwise a static method may be more suitable

```py
  class Employee:
      def __init__(self, first, last):
          self.first = first
          self.last = last

      def add_area(self, area):
          self.area = area

  employee_1 = Employee("Daniel", "Vilela")
  employee_1.add_area("Finance")
```

### Define a static method

Sometimes you may want to create a **method that has** some **logical relation
to** our **class but** is **not dependent on** any specific instance or class
variable there fore it does not need the `self` or `cls` objects passed to it

For this you use the `@staticmethod` decorator

```py
  <..>

    @staticmethod
    def is_workday(day):
        if day.weekday() == 5 or day.weekday() == 6:
            return False
        return True

  <..>
  import datetime

  my_date = datetime.date(2016, 7, 10)
  print(Employee.is_workday(my_date))       # True
```

### Define a class method

Class method are **tied to the whole class** itself and are **available to
all** it's **instances**. They are **identify by** the `@classmethod` [decorator](./ff01.md)

They are **most commonly used** for:

- Provide **alternative ways** to **create** an **instance** of your class
- Operate on **class variables**

```py
  class Employee:
      def __init__(self, first, last, pay):
          self.first = first
          self.last = last
          self.pay = pay

      @classmethod
      def from_string(cls, employee_string):
          first, last, pay = employee_string.split("-")
          return cls(first, last, int(pay))

  employee_1 = Employee("Daniel", "Vilela", 1200)
  employee_2 = Employee.from_string("Mario-Cubas-980")
```

### Define class variables

While each instance of a class can have it's own attributes, you can also
define **class variables** that **affect** the whole class **and shared by
all** it's **instances**

You just need to define them **inside the class** separate from any other method
definition. They are most commonly define **at the beginning of the class**
definition.

```py
  class Employee:
      raise_amount = 1.04
      num_of_employees = 0
```

To access them you can either:

- Call them from **within** the **class definition** as attributes of the class object

```py
  class Employee:
      num_of_employees = 0

      def __init__(self, first, last):
          self.first = first
          self.last = last

      Employee.num_of_employees += 1
```

- Access them **from** a **class instance**

```py
  employee_1 = Employee("Daniel", "Vilela")
  print(employee_1.num_of_employees)            # 1
```

They do **not conflict with an instance attributes** even if they have the same
name. You just have to be **mindful** whether you are **calling** the attribute **from**
the **class or** the **instance**

```py
  class Employee:
      raise_amount = 1.04

      def __init__(self, first, last, special_raise=self.raise_amount):
          self.first = first
          self.last = last
          self.raise_amount = special_raise


  employee_1 = Employee("Daniel", "Vilela", 1.02)
  print(Employee.raise_amount)                      # 1.04
  print(employee_1.raise_amount)                    # 1.02
```

### Referencing a class variable inside it's definition (best practice)

When you **reference an attribute** of an instance `Python` will **look for** that
attribute **on the class hierarchy or create it** if it doesn't exist anywhere on
the class or it's parents

So it's **best practice to** still **reference class variable** by the
`self.<class-variable>` instead of by `<Class-name>.<class-variable`

That way if the user manually changes the attribute it will override the class
variable and behave as expected

```py
  class Employee:
      raise_amount = 1.04

      def __init__(self, first, last, pay):
          self.first = first
          self.last = last
          self.pay = pay

      def raise_pay(self):
          self.pay = self.pay * self.raise_amount

  employee_1 = Employee("Daniel", "Vilela", 1000)
  employee_1.raise_amount = 1.05
  employee_1.raise_pay()
  print(employee_1.pay)             # 1050
```

### Create a subclass (inherit from parent class)

If you want a **subclass** (child) to **inherit** the **attributes** and
**methods** from **anothe class** (parent).

For example you may have **some** methods and attributes that you want **all**
off your classes to **share** but want **other subclasses** to have
**distinct** attributes and methods

**To** get **acces** to the **atributes from** the **parent** class you will
need to **use** the `super()` function

This will **also** inherit any **class variables** that where defined in the
parent class and **execute** all the **code inside** the parents `__init__`
function

```py
  class Manager(Employee):
      def __init__(self, first, last, pay, employees=None):
          super().__init__(first, last, pay)
          # You never want to pass mutable data types (list, dicts) as default args
          if employees is None:
              self.employees = []
          else:
              self.employees = employees

      def add_emp(self, emp):
          if emp not in self.employees:
              self.employees.append(emp)

      def remove_emp(self, emp):
          if emp in self.employees:
              self.employees.remove(emp)

      def list_emps(self):
          for emp in self.employees:
              print("--->", emp.full_name())


  manager_1 = Manager("Juan", "Gambino", 2000, [employee_1, employee_2])
```

### Create a singleton class

You can create a singleton class by storing the first instance of
the class as an attribute. Later attempts at creating an instance
simply return the stored instance

- In this case we are going to do it using a [decorator](./ff01.md) that wraps
  and turns a class into a singleton class

```py
  import functools

  def singleton(cls):
      """Make a class a Singleton class (only one instance)"""
      @functools.wraps(cls)
      def wrapper_singleton(*args, **kwargs):
          if not wrapper_singleton.instance:
              wrapper_singleton.instance = cls(*args, **kwargs)
          return wrapper_singleton.instance
      wrapper_singleton.instance = None
      return wrapper_singleton

  @singleton
  class TheOne:
      pass

  first_one = TheOne()
  another_one = TheOne()

  id(first_one)             # 140094218762280
  id(another_one)           # 140094218762280

  first_one is another_one  # True
```

> NOTE: Singleton classes are not really used as often in Python as
> in other languages. The effect of a singleton is usually better
> implemented as a global variable in a module.

### Find all the attributes that belong to an specific object

You can use a special **magic attribute** `__dict__` to display all the
**attributes** that **belong** to an **object** (be it class or instance)

It will **convert** all your **attributes** in a **{key: value} pair** [dictionary](./0loj.md)
format. So it's **great for** debugging and testing purposes

```py
  print(Employee.__dict__)      # All the atributes for class level
  print(employee_1.__dict__)    # All atributes for instance level
```

### Check if an object is an instance of a class

If you **use** the `isinstance()` **built-in** to check if an object is an
instance of a class. This is also a **good way** to **determine** if a **value
is of** a certain **type**

```py
  value = 5
  print(isinstance(value, int))     # True
```

### Define read only attributes (Encapsulation)(Getters)

- This in **OOP** terms is defined as **encapsulation**:

**Attributes** for which only got **one opportunity** for **setting** their
**value** and then we can't change the value anymore. This is usefull if we
don't want our users to mess with the values of the class instance after it has
been instantiated

To define an encapsulated attribute we **created using** a method with the
`@property` decorator

Then when we **define** our attribute value **for the first** time we need to
**prefix** `_` before the attribute name to enable us to define our
encapsulated attribute based on a regular attribute

But the `_` prefixed attribute could still be accesible as an attribute to the
class instance. If we want to **prevent total acces** to the attribute is we can
prefix it with **double underscores** (`__`) to **turn** it into a **private attribute**

```py
  class Employee:
      def __init__(self, first, last, pay):
          self.__first = first
          self._last = last
          self.pay = pay

      @property
      def first(self):
          [<extra-code-to-be-excecuted]
          return self.__first

      @property
      def last(self):
          print("Hello")
          return self._last

  employee_1 = Employee("Daniel", "Vilela", 1000)
  print(employee_1.__first)                         # Can't acces __first
  print(employee_1._last)                           # "Vilela"
  print(employee_1.first)                           # "Daniel"
  employee_1.first = "Juan                          # Can't modify atribute
  print(employee_1.last)                            # "Hello"\n"Vilela"
```

### Define a setter for an encapsulated attribute (Setter)

When you difine a **property** (encapsultaed attribute) it's value can't be
changed later through the normal means.

If you want to do so you will need to define a **setter function**. This
function will **allow you to change** the value of the **property** when called.

You implemented by using a special **decorator** `@<attribute-name>.setter`

```py
  class Employee:
      def __init__(self, first, last, pay):
          self.__first = first
          self._last = last
          self.pay = pay

      @property
      def first(self):
          return self.__first

      @property
      def last(self):
          return self._last

      @first.setter
      def first(self, value):
          [<extra-code-to-be-excecuted]
          self.__first = value

      @last.setter
      def last(self, value):
          print(value[0])
          self._last = value

  employee_1 = Employee("Daniel", "Vilela", 1000)
  print(employee_1.first)                           # "Daniel"
  employee_1.first = "Jose"
  print(employee_1.first)                           # "Jose"
  employee_1.last = "Moreno"                        # "M"
  print(employee_1.last)                            # "Moreno"
```

### Restrict the values that can be passed to an attribute

A **good use for setters** is for **restricting** what **values** can be given
to the attributes of an instance of a class **after** it has been **instantiated**

```py
  class Employee:
      def __init__(self, first, last, pay):
          self._first = first
          self.last = last
          self.pay = pay

      @property
      def first(self):
          return self.__first

      @first.setter
      def first(self, value):
          if value.isdigit():
              raise ValueError("Can't asign numbers to first name")
          else:
              self.__first = value

  employee_1 = Employee("Daniel", "Vilela", 1000)
  employee_1.first = "135"                      # "Can't asign numbers to first name"
```

### Define private methods

This are methods that you **don't want** the **user** of your class **to have
acces** to. Since it might be that you only need them inside the logic of your
class definition

This is called **abstraction** in which we **only exposed** to the user the
attributes and methods that are **relevant** to the user

The way we **achive this** is by **prefixing double underscore** (`__`) before the
method name

```py
  class Employee:
      def __init__(self, first, last):
          self.first = first
          self.last = last

      def __myPrivateMethod(self):
          <some-logic>
```
