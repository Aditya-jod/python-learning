# Object-Oriented Programming (OOP) in Python

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects", which can contain data in the form of fields (often known as attributes or properties) and code in the form of procedures (often known as methods).

The main idea of OOP is to bind data and the functions that work on that data together into a single unit (an object) so that no other part of the code can access this data except through that unit's functions.

---

## 1. Classes and Objects

-   **Class**: A blueprint for creating objects. It defines a set of attributes and methods that the created objects will have.
-   **Object (or Instance)**: An instance of a class. It's a concrete entity created from the class blueprint, with actual values for its attributes.

### Example: Creating a `Dog` Class

```python
# Define a class called Dog
class Dog:
    # A simple class attribute
    species = "Canis familiaris"

    # The constructor method, called when a new object is created
    def __init__(self, name, age):
        # These are instance attributes
        self.name = name
        self.age = age

    # An instance method
    def bark(self):
        return "Woof!"

# --- Creating Objects (Instances) ---

# Create two Dog objects from the Dog class blueprint
dog1 = Dog("Buddy", 3)
dog2 = Dog("Lucy", 5)

# Accessing instance attributes
print(f"{dog1.name} is {dog1.age} years old.") # Output: Buddy is 3 years old.
print(f"{dog2.name} is {dog2.age} years old.") # Output: Lucy is 5 years old.

# Accessing a class attribute
print(f"They are both of the species: {dog1.species}") # Output: They are both of the species: Canis familiaris

# Calling an instance method
print(f"{dog1.name} says: {dog1.bark()}") # Output: Buddy says: Woof!
```

-   `__init__` is the special **constructor** method. It's called automatically when you create a new instance of the class.
-   `self` refers to the current instance of the class (`dog1` or `dog2` in this case). It's used to access attributes and methods of the instance.

---

## 2. The Four Pillars of OOP

OOP is built on four fundamental principles: Inheritance, Encapsulation, Polymorphism, and Abstraction.

### a) Inheritance

Inheritance allows a new class (the **child class** or **subclass**) to inherit attributes and methods from an existing class (the **parent class** or **superclass**). This promotes code reuse.

```python
# Parent class
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        raise NotImplementedError("Subclass must implement this abstract method")

# Child class 'Dog' inherits from 'Animal'
class Dog(Animal):
    def speak(self):
        return f"{self.name} says Woof!"

# Child class 'Cat' inherits from 'Animal'
class Cat(Animal):
    def speak(self):
        return f"{self.name} says Meow!"

my_dog = Dog("Buddy")
my_cat = Cat("Whiskers")

print(my_dog.speak()) # Output: Buddy says Woof!
print(my_cat.speak()) # Output: Whiskers says Meow!
```

### b) Encapsulation

Encapsulation is the bundling of data (attributes) and the methods that operate on that data into a single unit (the class). It also involves restricting direct access to some of an object's components, which is a key part of data hiding.

In Python, encapsulation is achieved through naming conventions:
-   `_protected_attribute`: A single underscore prefix indicates that an attribute is "protected" and should not be accessed directly from outside the class. It's a convention.
-   `__private_attribute`: A double underscore prefix "mangles" the attribute name, making it much harder to access from outside the class.

```python
class Car:
    def __init__(self, make, model):
        self.make = make # Public attribute
        self._model = model # Protected attribute
        self.__engine_status = "Off" # Private attribute

    def start_engine(self):
        self.__engine_status = "On"
        print("Engine started.")

    def get_engine_status(self):
        return self.__engine_status

my_car = Car("Toyota", "Camry")

# Accessing public attribute is fine
print(my_car.make) # Output: Toyota

# Accessing protected attribute is possible, but discouraged by convention
print(my_car._model) # Output: Camry

# Accessing private attribute directly will fail
# print(my_car.__engine_status) # AttributeError: 'Car' object has no attribute '__engine_status'

# Access private data through a public method (getter)
my_car.start_engine()
print(f"Engine is {my_car.get_engine_status()}") # Output: Engine is On
```

### c) Polymorphism

Polymorphism means "many forms". In OOP, it refers to the ability of different objects to respond to the same method call in their own unique ways.

In the Inheritance example above, both `Dog` and `Cat` objects have a `speak()` method. We can call `speak()` on either object, and it will behave correctly for that object's type.

```python
def make_animal_speak(animal):
    # We don't need to know if the animal is a Dog or a Cat.
    # We just need to know that it has a .speak() method.
    print(animal.speak())

my_dog = Dog("Buddy")
my_cat = Cat("Whiskers")

make_animal_speak(my_dog) # Output: Buddy says Woof!
make_animal_speak(my_cat) # Output: Whiskers says Meow!
```
This makes the code more flexible and decoupled.

### d) Abstraction

Abstraction means hiding the complex implementation details and showing only the essential features of the object. It's about simplifying a complex system by modeling classes appropriate to the problem.

In the Inheritance example, the `Animal` class is an **abstraction**. It defines what an animal can do (`speak()`) but doesn't specify *how*. The concrete subclasses (`Dog`, `Cat`) provide the specific implementation.

Using `raise NotImplementedError` in the parent class is a simple way to enforce that child classes must provide their own implementation for an abstract method. For more formal abstraction, Python provides the `abc` (Abstract Base Classes) module.

```python
from abc import ABC, abstractmethod

class Shape(ABC): # Inherit from ABC to make it an abstract base class
    @abstractmethod
    def area(self):
        pass

class Square(Shape):
    def __init__(self, side):
        self.side = side
    
    def area(self):
        return self.side * self.side

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius * self.radius

# You cannot create an instance of an abstract class
# my_shape = Shape() # TypeError: Can't instantiate abstract class Shape with abstract method area

my_square = Square(5)
print(f"Square area: {my_square.area()}") # Output: Square area: 25
```
Abstraction helps manage complexity by providing a clear and simple interface.
