---
title: Python OOP
date: 2025-03-19T23:26:32+07:00
lastmod: 2025-03-19T23:26:32+07:00
author: Indra Sudirman
avatar: /img/indra.png
# authorlink: https://author.site
cover: python-oop.png
# images:
#   - /img/cover.jpg
categories:
  - python
tags:
  - python
  - oop
# nolastmod: true
draft: false
---

Just my notes about Python OOP.

<!--more-->

<p align="center">﷽</p>

## Python OOP

### Reserved Words

In Python, there are some reserved words that cannot be used as variable names, function names, or any other identifiers. These reserved words are called _reserved words_. Here is the complete list of Python's reserved words:

| Keyword | Keyword  | Keyword | Keyword  | Keyword |
| ------- | -------- | ------- | -------- | ------- |
| False   | await    | else    | import   | pass    |
| None    | break    | except  | in       | raise   |
| True    | class    | finally | is       | return  |
| and     | continue | for     | lambda   | try     |
| as      | def      | from    | nonlocal | while   |
| assert  | del      | global  | not      | with    |
| async   | elif     | if      | or       | yield   |

For more details about these keywords, you can refer to the [Python documentation](https://docs.python.org/3/reference/lexical_analysis.html#keywords).

### Class

To create class in Python, we can use the following syntax:

```python
1 class ClassName:
2    pass
3
4 new_object = ClassName()
5 print(new_object)
```

> please noted the keyword `pass` in the line 2, it is used to create empty class, since we don't want to add any method or attribute to the class. So we use the keyword `pass`. `pass` is a reserved word in Python.

How about if we don't add the keyword `pass`? The Python interpreter will raise an error.

```python
new_object = MyClass()
    ^^^
IndentationError: expected an indented block after class definition on line 1
```

Please observe the error message. The error message says that we need to add an indented block _after class definition on line 1_. This is because we need to add at least one line of code after the class definition **since the class shouldn't be empty.**

### Properties and Class

In Python, we can create properties in the class. Properties are like variables that are associated with the class. We can use the following syntax to create properties in the class:

```python
class Student:
    name = None
    age = None
    major = None
```

in the class above, we create 3 properties (as class variables): `name`, `age`, and `major`.

> please noted that the keyword `None` is [reserved word in Python](#reserved-words), it is used to create empty properties. Since we don't want to add any value to the properties, we use the keyword `None`.

How about if we don't add the keyword _None_?

```python
class Student:
    name
    age
    major
```

The Python interpreter will raise an error.

```python
line 2, in Student
    name
NameError: name 'name' is not defined
```

There two way to assign value to the properties:

1. Assign value to the properties in the class

```python
class Student:
    name = "Indra"
    age = 20
    major = "Computer Science"
```

2. Assign value to the properties in the object

```python
class Student:
    name = None
    age = None
    major = None

Indra = Student()
Indra.name = "Indra"
Indra.age = 20
Indra.major = "Computer Science"
```

### Initializing Objects

When we create an object of a class, we can initialize the object by using the `__init__` method. The `__init__` method is used to initialize the object. The `__init__` method is called automatically when an object is created.

> If you have learned Java, you will find the `__init__` method similar to the constructor in Java. **The double underscore before and after the word** `init` is a convention in Python to indicate that the method is a special method. So the Pyhton interpreter will treat as special case.

The initializer is special method because it's doesn't have a return type. The first parameter of the `__init__` method is always `self`. The `self` parameter is a reference to the current object being initialized.

Let's see the example:

```python
1 class Student:
2    # Create initializer for Student class
3    def __init__(self, name, age, major):
4        self.name = name
5        self.age = age
6        self.major = major
7
8 # Create instance of Student class
9 Indra = Student("Indra", 20, "Math")
10 # Print instance variables
11 print(Indra)
```

the output will look like this:

```bash
<__main__.Student object at 0x102b29a90>
```

this occurs because the Python interpreter print the default string representation of the object not the property values.

to solve this problem, we can use:

1. `__str__` method

```python
# Define __str__ method
    def __str__(self):
        return f"Student(name={self.name}, age={self.age}, major={self.major})"
```

2. `__repr__` method

```python
def __repr__(self):
        return f"Student('{self.name}', {self.age}, '{self.major}')"
```

3. `vars()` built-in function

```python
def __str__(self):
    return str(vars(self))
```

I will use the `vars()` built-in function in this example.

```python
1 class Student:
2    # Create initializer for Student class
3    def __init__(self, name, age, major):
4        self.name = name
5        self.age = age
6        self.major = major
7
8    # vars(object) is a built-in function that returns a dictionary containing all attributes (properties) of an object.
9    def __str__(self):
10        return str(vars(self))
11
12 # Create instance of Student class
13 Indra = Student("Indra", 20, "Math")
14 # Print instance variables
15 print(Indra)
```

the output will look like this:

```bash
{'name': 'Indra', 'age': 20, 'major': 'Math'}
```

To be continued...
