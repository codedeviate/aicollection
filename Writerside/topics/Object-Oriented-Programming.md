# Object-Oriented Programming

## What is Object-Oriented Programming?

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects", which can contain data and code. Data is in the form of fields (often known as attributes or properties), and code is in the form of procedures (often known as methods).

## Key Principles of OOP

1. **Encapsulation**: Bundling the data (attributes) and methods (functions) that operate on the data into a single unit or class. It restricts direct access to some of the object's components.
2. **Abstraction**: Hiding the complex implementation details and showing only the necessary features of the object.
3. **Inheritance**: Mechanism by which one class can inherit the attributes and methods from another class, promoting code reuse.
4. **Polymorphism**: Ability to present the same interface for different underlying data types. It allows methods to do different things based on the object it is acting upon.

## Example of OOP Concepts

### Class and Object

A class is a blueprint for creating objects. An object is an instance of a class.

```python
class Animal:
    def __init__(self, name, species):
        self.name = name
        self.species = species

    def make_sound(self):
        pass

class Dog(Animal):
    def make_sound(self):
        return "Bark"

class Cat(Animal):
    def make_sound(self):
        return "Meow"

# Creating objects
dog = Dog("Buddy", "Canine")
cat = Cat("Whiskers", "Feline")

print(dog.name)  # Output: Buddy
print(dog.make_sound())  # Output: Bark
print(cat.name)  # Output: Whiskers
print(cat.make_sound())  # Output: Meow
```

In this example:
- **Encapsulation**: The `Animal` class encapsulates the attributes `name` and `species` and the method `make_sound`.
- **Abstraction**: The `make_sound` method is defined in the `Animal` class but implemented in the `Dog` and `Cat` subclasses.
- **Inheritance**: The `Dog` and `Cat` classes inherit from the `Animal` class.
- **Polymorphism**: The `make_sound` method behaves differently based on whether it is called on a `Dog` or `Cat` object.