# Patterns

Here are some common design patterns in software development:

1. **Creational Patterns**:
    - **Singleton**: Ensures a class has only one instance and provides a global point of access to it.
    - **Factory Method**: Defines an interface for creating an object but lets subclasses alter the type of objects that will be created.
    - **Abstract Factory**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
    - **Builder**: Separates the construction of a complex object from its representation, allowing the same construction process to create different representations.
    - **Prototype**: Creates new objects by copying an existing object, known as the prototype.

2. **Structural Patterns**:
    - **Adapter**: Allows incompatible interfaces to work together by converting the interface of a class into another interface that a client expects.
    - **Bridge**: Separates an object’s abstraction from its implementation so that the two can vary independently.
    - **Composite**: Composes objects into tree structures to represent part-whole hierarchies, allowing clients to treat individual objects and compositions uniformly.
    - **Decorator**: Adds additional responsibilities to an object dynamically, providing a flexible alternative to subclassing for extending functionality.
    - **Facade**: Provides a simplified interface to a complex subsystem, making it easier to use.
    - **Flyweight**: Reduces the cost of creating and manipulating a large number of similar objects by sharing common parts of the state between multiple objects.
    - **Proxy**: Provides a surrogate or placeholder for another object to control access to it.

3. **Behavioral Patterns**:
    - **Chain of Responsibility**: Passes a request along a chain of handlers, where each handler decides either to process the request or to pass it to the next handler in the chain.
    - **Command**: Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.
    - **Interpreter**: Defines a grammatical representation for a language and provides an interpreter to deal with this grammar.
    - **Iterator**: Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
    - **Mediator**: Defines an object that encapsulates how a set of objects interact, promoting loose coupling by keeping objects from referring to each other explicitly.
    - **Memento**: Captures and externalizes an object’s internal state without violating encapsulation, so that the object can be restored to this state later.
    - **Observer**: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
    - **State**: Allows an object to alter its behavior when its internal state changes, appearing to change its class.
    - **Strategy**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable, allowing the algorithm to vary independently from clients that use it.
    - **Template Method**: Defines the skeleton of an algorithm in a method, deferring some steps to subclasses without changing the algorithm’s structure.
    - **Visitor**: Represents an operation to be performed on the elements of an object structure, allowing new operations to be defined without changing the classes of the elements on which it operates.