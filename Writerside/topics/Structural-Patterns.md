# Structural Patterns

Structural patterns are design patterns that ease the design by identifying a simple way to realize relationships between entities. They help ensure that if one part of a system changes, the entire system doesn't need to change. Here are some common structural patterns with examples in a generic language:

## 1. Adapter
Allows incompatible interfaces to work together by converting the interface of a class into another interface that a client expects.

```generic
// Target interface
interface Target {
    func request()
}

// Adaptee class
class Adaptee {
    func specificRequest() {
        // Implementation
    }
}

// Adapter class
class Adapter: Target {
    var adaptee: Adaptee

    init(adaptee: Adaptee) {
        self.adaptee = adaptee
    }

    func request() {
        adaptee.specificRequest()
    }
}
```

## 2. Bridge
Separates an object’s abstraction from its implementation so that the two can vary independently.

```generic
// Abstraction
abstract class Shape {
    var color: Color

    init(color: Color) {
        self.color = color
    }

    abstract func applyColor()
}

// Implementor
interface Color {
    func fill()
}

// Concrete Implementor
class RedColor: Color {
    func fill() {
        // Fill with red color
    }
}

// Refined Abstraction
class Circle: Shape {
    func applyColor() {
        color.fill()
    }
}
```

## 3. Composite
Composes objects into tree structures to represent part-whole hierarchies, allowing clients to treat individual objects and compositions uniformly.

```generic
// Component
interface Graphic {
    func draw()
}

// Leaf
class Circle: Graphic {
    func draw() {
        // Draw circle
    }
}

// Composite
class CompositeGraphic: Graphic {
    var graphics: [Graphic] = []

    func add(graphic: Graphic) {
        graphics.append(graphic)
    }

    func remove(graphic: Graphic) {
        graphics.removeAll { $0 === graphic }
    }

    func draw() {
        for graphic in graphics {
            graphic.draw()
        }
    }
}
```

## 4. Decorator
Adds additional responsibilities to an object dynamically, providing a flexible alternative to subclassing for extending functionality.

```generic
// Component
interface Coffee {
    func cost() -> Double
}

// Concrete Component
class SimpleCoffee: Coffee {
    func cost() -> Double {
        return 1.0
    }
}

// Decorator
abstract class CoffeeDecorator: Coffee {
    var decoratedCoffee: Coffee

    init(coffee: Coffee) {
        self.decoratedCoffee = coffee
    }

    func cost() -> Double {
        return decoratedCoffee.cost()
    }
}

// Concrete Decorator
class MilkDecorator: CoffeeDecorator {
    func cost() -> Double {
        return super.cost() + 0.5
    }
}
```

## 5. Facade
Provides a simplified interface to a complex subsystem, making it easier to use.

```generic
class Facade {
    var subsystem1: Subsystem1
    var subsystem2: Subsystem2

    init() {
        self.subsystem1 = Subsystem1()
        self.subsystem2 = Subsystem2()
    }

    func operation() {
        subsystem1.operation1()
        subsystem2.operation2()
    }
}

class Subsystem1 {
    func operation1() {
        // Implementation
    }
}

class Subsystem2 {
    func operation2() {
        // Implementation
    }
}
```

## 6. Flyweight
Reduces the cost of creating and manipulating a large number of similar objects by sharing common parts of the state between multiple objects.

```generic
class Flyweight {
    var intrinsicState: String

    init(intrinsicState: String) {
        self.intrinsicState = intrinsicState
    }

    func operation(extrinsicState: String) {
        // Use intrinsicState and extrinsicState
    }
}

class FlyweightFactory {
    var flyweights: [String: Flyweight] = [:]

    func getFlyweight(key: String) -> Flyweight {
        if flyweights[key] == nil {
            flyweights[key] = Flyweight(intrinsicState: key)
        }
        return flyweights[key]!
    }
}
```

## 7. Proxy
Provides a surrogate or placeholder for another object to control access to it.

```generic
// Subject interface
interface Subject {
    func request()
}

// RealSubject class
class RealSubject: Subject {
    func request() {
        // Implementation
    }
}

// Proxy class
class Proxy: Subject {
    var realSubject: RealSubject?

    func request() {
        if realSubject == nil {
            realSubject = RealSubject()
        }
        realSubject?.request()
    }
}
```

These patterns help in structuring code in a way that reduces complexity and increases flexibility and maintainability.