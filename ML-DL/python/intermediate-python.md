## Intermediate Python:

## **1. Object-Oriented Programming (OOP):**

OOP is a programming paradigm that provides a means of structuring programs so that properties and behaviors are bundled into individual objects.

- **Classes and Objects:**

A class is a code template for creating objects. Objects have member variables and have behavior associated with them. In python, a class is created by the keyword `class`.

```python
class MyClass:
    x = 5

p1 = MyClass()  # p1 is an object of MyClass
print(p1.x)  # Output: 5
```

- **Inheritance:**

Inheritance allows us to define a class that inherits all the methods and properties from another class. Parent class is the class being inherited from, also called base class. Child class is the class that inherits from another class, also called derived class.

```python
class Person:
    def __init__(self, fname):
        self.firstname = fname

    def printname(self):
        print(self.firstname)

class Student(Person):
    pass  # Use the pass keyword when you do not want to add any other properties or methods to the class.

x = Student("Mike")
x.printname()  # Output: Mike
```

- **Encapsulation:**

We can restrict access to methods and variables. This prevents data from direct modification which is called encapsulation. In Python, we denote private attributes using underscore as the prefix i.e single `_` or double `__`.

```python
class Computer:

    def __init__(self):
        self.__maxprice = 900

    def sell(self):
        print("Selling Price: {}".format(self.__maxprice))

    def setMaxPrice(self, price):
        self.__maxprice = price

c = Computer()
c.sell()  # Output: Selling Price: 900

# change the price
c.__maxprice = 1000
c.sell()  # Output: Selling Price: 900

# using setter function
c.setMaxPrice(1000)
c.sell()  # Output: Selling Price: 1000
```

- **Polymorphism:**

Polymorphism is an ability (in OOP) to use a common interface for multiple forms (data types).

Suppose, we need to color a shape, there are multiple shape options (rectangle, square, circle). However we could use the same method to color any shape. This concept is called Polymorphism.

```python
class Parrot:

    def fly(self):
        print("Parrot can fly")

    def swim(self):
        print("Parrot can't swim")

class Penguin:

    def fly(self):
        print("Penguin can't fly")

    def swim(self):
        print("Penguin can swim")

# common interface
def flying_test(bird):
    bird.fly()

# instantiate objects
blu = Parrot()
peggy = Penguin()

# passing the object
flying_test(blu)  # Output: Parrot can fly
flying_test(peggy)  # Output: Penguin can't fly
```

### **2. Functional Programming:**

Python allows you to use functional programming paradigms, and provides several functions and constructs that mirror capabilities of functional languages.

- **Lambda Functions:**

Lambda functions are small, anonymous functions that are defined with the lambda keyword.

```python
add = lambda x, y: x + y
print(add(5, 3))  # Output: 8
```

- **Map, Reduce, and Filter:**

The `map`, `reduce` and `filter` functions all operate on lists, allowing you to transform or filter out elements in a concise manner.

```python
numbers = [1, 2, 3, 4, 5]
squared = map(lambda x: x ** 2, numbers)  # Output: [1, 4, 9, 16, 25]

from functools import reduce
product = reduce((lambda x, y: x * y), numbers)  # Output: 120

even_numbers = filter(lambda x: x%2 == 0, numbers)  # Output: [2, 4]
```

### **3. List Comprehensions, Dictionary Comprehensions:**

List comprehensions provide a concise way to create lists. It consists of brackets containing an expression followed by a for statement, then zero or more for or if clauses.

```python
squares = [x**2 for x in range(10)]  # Output: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

dict_squares = {x: x**2 for x in range(5)}  # Output: {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

### **4. Modules and Packages:**

Modules in Python are simply Python files with a .py extension. The name of the module will be the name of the file. A Python module can have a set of functions, classes or variables defined and implemented.

Packages are a way of structuring Python’s module namespace by using “dotted module names”.

```python
# Importing a module
import math
print(math.pi)  # Output: 3.141592653589793

# Importing a function
from math import pi
print(pi)  # Output: 3.141592653589793

# Installing and using packages
# Use pip to install a package. For example to install numpy, you would use:
# pip install numpy

import numpy as np
print(np.array([1, 2, 3]))  # Output: array([1, 2, 3])
```

Here is a simple way to create a module:

Create a file named mymodule.py in a text editor, and write the following code inside it:

```python
def greeting(name):
print(f"Hello, {name}!")

def sum_numbers(a, b):
return a + b
```

1. Save the file in the directory where you'll write your main Python file.
2. Now you can use the module you just created, by using the import statement:

Create a new Python file, and import the module you just created:

```python
import mymodule

mymodule.greeting("Alice")
print(mymodule.sum_numbers(1, 2))
```

It's important to note that modules should be placed in the same directory as the file, or in a Python path directory, for Python to be able to locate them. If they are in another directory, the directory should be added to PYTHONPATH.

Furthermore, Python packages are a way of organizing related modules into a directory hierarchy. Essentially, a package is a directory with Python files and a file with the name **init**.py. This file can be empty, and it indicates that the directory it contains is a Python package, so it can be imported the same way a module can be imported.

### **5. Debugging and Testing:**

Python has several tools for debugging and testing: pdb for debugging, unittest and pytest for testing.

#### **pdb**:

pdb is the Python debugger, and is a powerful interactive debugger which allows you to step through the code, set breakpoints, watch variables etc.

You can set breakpoints in your code where you want to start debugging. Breakpoints are points in your code where you want the program execution to pause so you can inspect the state of your program. You can set breakpoints using the pdb.set_trace() function:

```python
# Using pdb
import pdb

def some_function():
    x = 5
    y = 0
    result = x / y  # This line will cause an error
    return result

pdb.set_trace()
result = some_function()
```

When your code reaches a line containing pdb.set_trace(), it will pause execution, and you will be dropped into the pdb debugger prompt. It looks like this:

```
> your_script.py(9)some_function()
-> result = x / y
(Pdb)
```

Here, you can enter debugger commands to inspect and control the debugging session.

**Debugging Commands:**
You can use various `pdb` commands to interact with your code while it's paused. Here are some common commands:

- `n` (next): Execute the current line and move to the next line of code.
- `c` (continue): Continue execution until the next breakpoint is encountered.
- `s` (step): Step into a function or method (if the current line calls a function).
- `q` (quit): Exit the debugger and terminate the program.
- `p` variable_name: Print the value of a variable.
- `l` (list): Show the code around the current line.
- `h` (help): Display a list of available commands.
  You can type these commands at the `(Pdb)` prompt to control the debugger's behavior.

You can use the p command followed by a variable name to print its value. For example:

```
(Pdb) p x
5
```

#### **unittest/pytest**:

`unittest` is a built-in module for testing in Python. You can write test cases, check output and automate testing work in your code. `pytest` is a third-party module for testing that's more flexible than unittest.

Let's look at an example of using unittest:

```python
# Using unittest
import unittest

def add(x, y):
    return x + y

class TestAdd(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(1, 2), 3)

if __name__ == '__main__':
    unittest.main()
```

**Assertions:**
unittest provides a variety of assertion methods to verify that the actual results match the expected results.

Here are some common assertion methods:

```python
self.assertEqual(actual, expected)
self.assertNotEqual(actual, expected)
self.assertTrue(condition)
self.assertFalse(condition)
self.assertRaises(exception, callable, *args, **kwargs)
```

**Running Tests:**
To run your tests, you typically execute your test script or module. The `unittest` framework will automatically discover and run all test methods within classes that inherit from `unittest.TestCase`. You can run your tests in various ways:

- Run the script directly:

  ```python
  if __name__ == "__main__":
      unittest.main()
  ```

- Use the command-line test runner:

  ```bash
  python -m unittest your_test_module
  ```

**_Setup and Teardown:_**
You can use `setUp` and `tearDown` methods to set up any preconditions for your tests or to clean up resources after each test method runs. These methods are defined in your test case class and are executed before and after each test method.

```python
import unittest

class MyTestCase(unittest.TestCase):
    def setUp(self):
        # Set up any resources or preconditions for tests
        self.data = [1, 2, 3]

    def tearDown(self):
        # Clean up resources or perform post-test actions
        self.data = None

    def test_something(self):
        # Test code that uses self.data
        pass
```

**Skipping and Expected Failures:**
`unittest` supports decorators like `@unittest.skip` to skip specific tests and `@unittest.expectedFailure` to mark tests that are expected to fail.

```python
import unittest

class MyTestCase(unittest.TestCase):
    @unittest.skip("This test is not implemented yet")
    def test_not_implemented(self):
        pass

    @unittest.expectedFailure
    def test_expected_failure(self):
        self.assertEqual(2 + 2, 5)
```

- **Test Discovery:**
  `unittest` has built-in test discovery mechanisms, which means it will search for test cases and methods to run based on naming conventions. Test methods should start with "test\_" for automatic discovery. Test cases are discovered based on classes that inherit from `unittest.TestCase`.

This should give you a solid foundation on intermediate Python. You can build upon this knowledge by exploring more advanced topics and techniques.
