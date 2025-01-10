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
```

---

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
```

---

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
