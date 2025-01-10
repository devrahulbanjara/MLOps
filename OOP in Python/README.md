<<<<<<< HEAD
# Object-Oriented Programming (OOP) in Python

Welcome to the **OOP in Python** repository! This README file will guide you through various OOP concepts in Python, using beginner-friendly examples and explanations.

## Table of Contents

1. [Importance of OOPs in Python for Data Science](#1-importance-of-oops-in-python-for-data-science)
2. [Introduction to Object-Oriented Programming in Python](#2-introduction-to-object-oriented-programming-in-python)
3. [Importance of Adding a README File](#3-importance-of-adding-a-readme-file)
4. [Understanding Object-Oriented Programming Concepts](#4-understanding-object-oriented-programming-concepts)
   - [Properties and Functionalities of a Phone Model](#properties-and-functionalities-of-a-phone-model)
   - [Class and Objects](#class-and-objects)
   - [Basics of Creating and Using Classes](#basics-of-creating-and-using-classes)
   - [Constructors and Object Creation](#constructors-and-object-creation)
   - [Encapsulation, Getters, and Setters](#encapsulation-getters-and-setters)
   - [Inheritance](#inheritance)
   - [Diamond Problem and Multiple Inheritance](#diamond-problem-and-multiple-inheritance)

---

## 1. Importance of OOPs in Python for Data Science

Object-Oriented Programming (OOP) helps in creating modular, reusable, and maintainable code. For data science, OOP can:

- Simplify complex data manipulations.
- Improve code readability.
- Facilitate teamwork by structuring code into manageable chunks.

Example:
```python
class DataProcessor:
    def __init__(self, data):
        self.data = data

    def mean(self):
        return sum(self.data) / len(self.data)

processor = DataProcessor([1, 2, 3, 4, 5])
print(processor.mean())  # Output: 3.0
=======
# Object-Oriented Programming (OOP) in Python for Data Science

## Introduction

Object-Oriented Programming (OOP) is a programming paradigm that organizes code into reusable "objects." Python’s flexibility and support for OOP make it one of the most popular languages for Data Science, enabling clean, modular, and reusable code.

In Data Science, OOP helps:
- **Model real-world problems**: Represent datasets, models, and operations as objects.
- **Reuse code**: Build classes for tasks like preprocessing, feature engineering, or model evaluation.
- **Organize projects**: Maintain scalable and maintainable codebases.

This guide will walk you through OOP concepts, progressing from beginner to advanced, with a focus on their applications in Data Science.

---

## Table of Contents
1. [Basics of OOP](#1-basics-of-oop)
2. [Constructors](#2-constructors)
3. [Dunder Methods](#3-dunder-methods)
4. [Inheritance](#4-inheritance)
5. [Abstract Base Classes](#5-abstract-base-classes)
6. [Polymorphism](#6-polymorphism)
7. [Encapsulation](#7-encapsulation)
8. [Static and Class Methods](#8-static-and-class-methods)
9. [Dynamic Typing vs. Static Type Checking](#9-dynamic-typing-vs-static-type-checking)
10. [Summary and Best Practices](#10-summary-and-best-practices)

---

## 1. Basics of OOP

### Classes and Objects
**Classes** are blueprints for creating objects. **Objects** are instances of classes.

**Analogy**: A class is like a recipe, and objects are the dishes you prepare using it.

```python
# Define a class
class DataScientist:
    def __init__(self, name, skill):
        self.name = name  # Instance variable
        self.skill = skill

# Create an object
scientist = DataScientist("Rahul", "Python")
print(scientist.name)  # Output: Rahul
```

### Variables and Functions
- **Instance variables** store data specific to each object.
- **Methods** are functions defined within classes.

```python
class DataScientist:
    def __init__(self, name, skill):
        self.name = name
        self.skill = skill

    def introduce(self):
        return f"Hi, I'm {self.name} and I specialize in {self.skill}."

scientist = DataScientist("Rahul", "Data Science")
print(scientist.introduce())  # Output: Hi, I'm Rahul and I specialize in Data Science.
>>>>>>> ReadmeforOOP
```

---

<<<<<<< HEAD
## 2. Introduction to Object-Oriented Programming in Python

OOP is a programming paradigm that revolves around objects and classes.

### Key Concepts:
- **Class**: Blueprint for creating objects.
- **Object**: Instance of a class.
- **Attributes**: Variables associated with an object.
- **Methods**: Functions defined inside a class.

Example:
```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def drive(self):
        print(f"The {self.brand} {self.model} is driving!")

my_car = Car("Toyota", "Corolla")
my_car.drive()  # Output: The Toyota Corolla is driving!
=======
## 2. Constructors

Constructors (“`__init__`” method) initialize an object when it’s created. They’re particularly useful for setting up initial states like model parameters or dataset paths.

```python
class Dataset:
    def __init__(self, data_path):
        self.data_path = data_path

    def load_data(self):
        return f"Loading data from {self.data_path}"

data = Dataset("data.csv")
print(data.load_data())  # Output: Loading data from data.csv
```

### Using `super` in Constructors
The `super` function allows you to call a method from a parent class. It's especially useful in constructors when dealing with inheritance, enabling the child class to extend the functionality of the parent class without rewriting code.

#### Why Use `super`?
1. To avoid explicitly naming the parent class, making your code more maintainable.
2. To ensure that the parent class's `__init__` method is properly called and initialized.
3. To handle multiple inheritance scenarios where the method resolution order (MRO) determines which parent class is called.

(Dont worry if you dont understand what is MRO, it has been explained in [Inheritance](#4-inheritance) with examples.)

#### Example: Single Inheritance
```python
class Model:
    def __init__(self, name):
        self.name = name
        print(f"Model {self.name} initialized")

class LinearRegression(Model):
    def __init__(self, name, parameters):
        super().__init__(name)  # Calls the parent class constructor
        self.parameters = parameters
        print(f"LinearRegression with parameters {self.parameters} initialized")

lr = LinearRegression("Linear Regression", {"alpha": 0.01})
# Output:
# Model Linear Regression initialized
# LinearRegression with parameters {'alpha': 0.01} initialized
```

#### Example: Multiple Inheritance
```python
class A:
    def __init__(self):
        print("Initializing A")

class B:
    def __init__(self):
        print("Initializing B")

class C(A, B):
    def __init__(self):
        super().__init__()  # Calls A's constructor due to MRO
        print("Initializing C")

c = C()
# Output:
# Initializing A
# Initializing C
>>>>>>> ReadmeforOOP
```

---

<<<<<<< HEAD
## 3. Importance of Adding a README File

A README file:
- Explains the purpose of your project.
- Guides users on how to use it.
- Enhances project professionalism and accessibility.

---

## 4. Understanding Object-Oriented Programming Concepts

### Properties and Functionalities of a Phone Model

Example:
```python
class Phone:
    def __init__(self, brand, model, price):
        self.brand = brand
        self.model = model
        self.price = price

    def make_call(self):
        print(f"Calling from {self.brand} {self.model}")

my_phone = Phone("Apple", "iPhone 14", 999)
my_phone.make_call()  # Output: Calling from Apple iPhone 14
```

### Class and Objects

A **class** defines a structure, and an **object** is an instance of that class.

Example:
```python
class Animal:
    def __init__(self, name):
        self.name = name

lion = Animal("Lion")
print(lion.name)  # Output: Lion
```

### Basics of Creating and Using Classes

Example:
```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

    def read(self):
        print(f"Reading {self.title} by {self.author}")

my_book = Book("1984", "George Orwell")
my_book.read()  # Output: Reading 1984 by George Orwell
```

### Constructors and Object Creation

Constructors initialize object attributes.

Example:
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

john = Person("John", 30)
print(john.name, john.age)  # Output: John 30
```

### Encapsulation, Getters, and Setters

Encapsulation hides implementation details. Getters and setters provide controlled access.

Example:
```python
class BankAccount:
    def __init__(self):
        self.__balance = 0

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance

account = BankAccount()
account.deposit(100)
print(account.get_balance())  # Output: 100
```

### Inheritance

Inheritance allows a class to reuse another class's functionality.

Example:
```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):
        print("Dog barks")

my_dog = Dog()
my_dog.speak()  # Output: Dog barks
```

### Diamond Problem and Multiple Inheritance

Python resolves the diamond problem using the Method Resolution Order (MRO).

Example:
```python
class A:
    def say(self):
        print("A says hello")

class B(A):
    def say(self):
        print("B says hello")

class C(A):
    pass

class D(B, C):
    pass

d = D()
d.say()  # Output: B says hello
=======
## 3. Dunder Methods

Dunder (double underscore) methods enable Python’s built-in functionality, like printing or adding objects.

### `__str__` and `__repr__`

- `__str__`: Provides a human-readable string representation of an object, suitable for end-users.
- `__repr__`: Provides an unambiguous string representation of an object, suitable for developers.

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"Vector with coordinates ({self.x}, {self.y})"

    def __repr__(self):
        return f"Vector(x={self.x}, y={self.y})"

v = Vector(1, 2)
print(str(v))  # Output: Vector with coordinates (1, 2)
print(repr(v))  # Output: Vector(x=1, y=2)

# Directly calling the object
print(v)        # Output: Vector with coordinates (1, 2)        (when there are both repr and str in a class, str will get called)
```

Why use `__str__` and `__repr__`?
- **`__str__`** is for end-users, presenting information in a user-friendly way.
- **`__repr__`** is for developers, providing an unambiguous and detailed representation to help debug and develop code.

### Adding with `__add__`

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)
v2 = Vector(3, 4)
print(v1 + v2)  # Output: Vector(4, 6)
```

---

## 4. Inheritance

Inheritance allows a class (child) to inherit methods and attributes from another class (parent).

```python
class Model:
    def __init__(self, name):
        self.name = name

    def train(self):
        return f"Training {self.name} model."

class LinearRegression(Model):
    def predict(self):
        return "Predicting with Linear Regression."

lr = LinearRegression("Linear Regression")
print(lr.train())  # Output: Training Linear Regression model.
print(lr.predict())  # Output: Predicting with Linear Regression.
```

#### Diamond Problem
Occurs when multiple inheritance creates ambiguity. Say Class D is inheriting from B and C classes, and both have the methods train(), then when D calls train, which class's train() will get called? Python resolves it using the **Method Resolution Order (MRO)**, meaning that C inherits the hello method from the first class it was passed, `A` from `A,B`.

```python
class A:
    def hello(self):
        print("Hello from A")

class B:
    def hello(self):
        print("Hello from B")

class C(A, B):
    pass

c = C()
c.hello()  # Output: Hello from A
```

---

## 5. Abstract Base Classes

ABCs define a blueprint for other classes. Abstract means methods of these classes are left unimplemented, and later it should be implemented by inheriting. If an abstract method is not implemented in a subclass that inherits from an **abstract base class (ABC)**, Python will raise a TypeError when trying to instantiate the subclass.

```python
from abc import ABC, abstractmethod

class Preprocessor(ABC):
    @abstractmethod
    def process(self, data):
        pass

class Scaler(Preprocessor):
    def process(self, data):
        return data / max(data)

scaler = Scaler()
print(scaler.process([1, 2, 3]))  # Example output
```

---

## 6. Polymorphism

**Polymorphism** allows objects of different classes to respond to the same method names in their own unique ways. This is a key feature of object-oriented programming (OOP) that promotes flexibility and reusability.

### Method Overloading

**Method Overloading** refers to defining multiple methods with the same name but different parameters. While Python does not support traditional method overloading (as seen in languages like Java or C++), you can achieve similar functionality by using default arguments or `*args` and `**kwargs`.

#### Example: Method overloading in Action

```python
class Calculator:
    def add(self, a, b, c=0):
        return a + b + c

calc = Calculator()
print(calc.add(2, 3))       # Output: 5
print(calc.add(2, 3, 4))    # Output: 9
```

### Method Overriding

**Method Overriding** occurs when a subclass provides a specific implementation of a method that is already defined in its parent class. This allows subclasses to customize or completely replace the behavior of the parent class's methods.

#### Example: Method overriding in Action

```python
class Animal:
    def speak(self):
        return "This animal makes a sound."

class Dog(Animal):
    def speak(self):
        return "Woof! Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

# Demonstrating method overriding
animals = [Animal(), Dog(), Cat()]
for animal in animals:
    print(animal.speak())
```

---

## 7. Encapsulation

Encapsulation is a principle that hides implementation details, making a program easier to maintain and less prone to errors. In Python, you can make variables private by adding a double underscore (`__`) prefix to the variable name (e.g., `__employeeSalary`). However, Python internally renames such variables using a process called **Name Mangling**. The variable name is transformed into `_<<classname>>__<<variablename>>`.

For example, if a class `A` has a variable named `__name`, it gets internally renamed to `_A__name`.

### Key Points:
- **Nothing is truly private in Python**: Sure, you can make variables "private" with some double underscores, but Python won't stop anyone determined enough to access them. Why? Because Python trusts you. As Guido van Rossum, the creator of Python, famously said:  
  *"Programmers are consenting adults."*  

  Translation: *"If you break it, it's your fault. Good luck!"*

### Example: Encapsulation with Name Mangling

```python
class Data:
    def __init__(self):
        self.__name = "Rahul"
    
    def get_name(self):
        return self.__name
    
    def set_name(self, name):
        self.__name = name

# Using the Data class
d = Data()
print(d.get_name())  # Output: Rahul
d.set_name("Subham")
print(d.get_name())  # Output: Subham
```

---

## 8. Static and Class Methods

- **Static methods** don’t require an instance.
- **Class methods** access class variables.

```python
class Metrics:
    @staticmethod
    def mean(values):
        return sum(values) / len(values)

    @classmethod
    def description(cls):
        return f"{cls.__name__} computes metrics."

print(Metrics.mean([1, 2, 3]))  # Output: 2.0
print(Metrics.description())  # Output: Metrics computes metrics.
```

---

## 9. Dynamic Typing vs. Static Type Checking

Python is dynamically typed, but type hints can improve code clarity (*Not a OOP concept but still adding it here*).

```python
# Without type hints
def add(a, b):
    return a + b

# With type hints
def add(a: int, b: int) -> int:
    return a + b
```

---

## 10. Summary and Best Practices

- Understand basics before diving into advanced concepts.
- Use OOP for reusable, organized, and scalable Data Science projects.
- Follow Pythonic conventions and write clear, concise code.

By mastering OOP, you’ll become more efficient in solving complex problems and developing robust Data Science pipelines.

>>>>>>> ReadmeforOOP
