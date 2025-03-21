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
  - programming language
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

#### Initializing Objects with Optional Parameters

We also can initialize an object with optional parameters. To initialize an object with optional parameters, we add **a default value to the parameter.** as follows:

```python
1 class Teacher:
2     # define the properties and assign None as default values
3    def __init__(self, name = None, age = None, subject = None):
4        self.name = name
5        self.age = age
6        self.subject = subject
```

Now let's try to create `Teacher` object:

```python
7 # Create instance of Teacher with default values
8 Bayu = Teacher()
9 # Print instance variables
10 print(Bayu)
11 # Create instance of Teacher and reassign values
12 Ibayu = Teacher("Ibayu", 20, "Math")
13 print(Ibayu)
```

The result will look like this for line 10 and 13:

```bash
{'name': None, 'age': None, 'subject': None}
{'name': 'Ibayu', 'age': 20, 'subject': 'Math'}
```

the first line result is print the default values of the properties otherwise the second line result is print the reassign values of the properties.

### Class Variables vs Instance Variables

Class variables are variables that are shared by all objects of a class. Instance variables are variables that are unique to each object of a class.

| Class Variable                                          | Instance Variable                                                            |
| ------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Declared in the class, outside of the `__init__` method | Declared in the `__init__` method                                            |
| Shared by all objects of the class                      | Unique to each object of the class                                           |
| All objects of the class will have the same value       | Each object of the class will have a different value, based on instantiation |

Here is the example:

```python
1 class Player:
2    nationalTeamName = "Indonesia" # class variable
3
4    def __init__(self, playerName):
5        self.playerName = playerName # instance variable
6
7    def __str__(self):
8        # concatenate class variable and instance variable
9        return str({"nationalTeamName": Player.nationalTeamName, **vars(self)})
10
11 Budi = Player("Budi")
12 print(Budi)
13
14 Bambang = Player("Bambang")
15 print(Bambang)
```

In the line 2 is **class variable**, in the line 5 is **instance variable**. Since we need to print the `nationalTeamName` so we should create method `__str__` (line 7 - 9) to print the class variable and instance variable.

The result will look like this:

```bash
{'nationalTeamName': 'Indonesia', 'playerName': 'Budi'}
{'nationalTeamName': 'Indonesia', 'playerName': 'Bambang'}
```

#### Bad Use of Class Variables

Imagine we have a class called `Company` as follows:

```python
1 class Company:
2     currentCompany = 'Google' # class variables
3     formerCompany = []
4
5     def __init__(self, name):
6        self.name = name # creating instance variables
7
8  c1 = Company('Rudi')
9  c1.formerCompany.append('Microsoft')
10 c2 = Company('Adam')
11 c2.formerCompany.append('Amazon')
12 print("Name:", c1.name)
13 print("Current Company:", c1.currentCompany)
14 print("Former Company:", c1.formerCompany)
15 print("Name:", c2.name)
16 print("Current Company:", c2.currentCompany)
17 print("Former Company:", c2.formerCompany)
```

the result will look like this:

```bash
Name: Rudi
Current Company: Google
Former Company: ['Microsoft', 'Amazon']
Name: Adam
Current Company: Google
Former Company: ['Microsoft', 'Amazon']
```

please observe that `Former Company` is shared by all objects of the class `Company`, so we should not use class variables to store data that is shared by all objects of the class. Since `Former Company` is unique to each object of the class, Rudi and Adam have different `Former Company`. The expected result is:

```bash
Name: Rudi
Current Company: Google
Former Company: ['Microsoft']
Name: Adam
Current Company: Google
Former Company: ['Amazon']
```

and the correct code should be **move the `formerCompany` variable to the `__init__` method** like this (line 7):

```python
1 class Company:
2     currentCompany = 'Google' # class variables
3
4
5     def __init__(self, name):
6        self.name = name # creating instance variables
7        self.formerCompany = []
8
9  c1 = Company('Rudi')
10 c1.formerCompany.append('Microsoft')
11 c2 = Company('Adam')
12 c2.formerCompany.append('Amazon')
13 print("Name:", c1.name)
14 print("Current Company:", c1.currentCompany)
15 print("Former Company:", c1.formerCompany)
16 print("Name:", c2.name)
17 print("Current Company:", c2.currentCompany)
18 print("Former Company:", c2.formerCompany)
```

To be continued...

```

```
