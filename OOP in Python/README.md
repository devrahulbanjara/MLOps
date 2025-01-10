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
   - Classes and Objects
   - Variables and Functions
2. [Intermediate OOP Concepts](#2-intermediate-oop-concepts)
   - Constructors
   - Dunder Methods
3. [Advanced OOP Concepts](#3-advanced-oop-concepts)
   - Inheritance
   - Abstract Base Classes
   - Polymorphism
   - Encapsulation
   - Static and Class Methods
   - Dynamic Typing vs. Static Type Checking
4. [Summary and Best Practices](#4-summary-and-best-practices)

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
```

---

## 2. Intermediate OOP Concepts

### Constructors
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

### Dunder Methods
Dunder (double underscore) methods enable Python’s built-in functionality, like printing or adding objects.

#### `__str__` and `__repr__`
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
```

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

## 3. Advanced OOP Concepts

### Inheritance
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
Occurs when multiple inheritance creates ambiguity. Python resolves it using the **Method Resolution Order (MRO)**.

```python
class A: pass
class B(A): pass
class C(A): pass
class D(B, C): pass
print(D.mro())
```

### Abstract Base Classes (ABC)
ABCs define a blueprint for other classes.

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

### Polymorphism
**Polymorphism** allows different classes to use the same method names.

```python
class Model:
    def evaluate(self):
        return "Evaluating model."

class NeuralNetwork(Model):
    def evaluate(self):
        return "Evaluating neural network."

models = [Model(), NeuralNetwork()]
for model in models:
    print(model.evaluate())
```

### Encapsulation
Encapsulation hides implementation details.

```python
class Data:
    def __init__(self):
        self._data = []  # Protected attribute

    def add(self, value):
        self._data.append(value)

    @property
    def data(self):
        return self._data

    @data.setter
    def data(self, value):
        if isinstance(value, list):
            self._data = value
        else:
            raise ValueError("Data must be a list.")
```

### Static and Class Methods
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

### Dynamic Typing vs. Static Type Checking
Python is dynamically typed, but type hints can improve code clarity.

```python
# Without type hints
def add(a, b):
    return a + b

# With type hints
def add(a: int, b: int) -> int:
    return a + b
```

---

## 4. Summary and Best Practices
- Understand basics before diving into advanced concepts.
- Use OOP for reusable, organized, and scalable Data Science projects.
- Follow Pythonic conventions and write clear, concise code.

By mastering OOP, you’ll become more efficient in solving complex problems and developing robust Data Science pipelines.