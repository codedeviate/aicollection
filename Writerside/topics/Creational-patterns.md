# Creational Patterns

Creational patterns are design patterns that deal with object creation mechanisms, trying to create objects in a manner suitable to the situation. They help make a system independent of how its objects are created, composed, and represented. Here are some common creational patterns with examples in a generic language:

## 1. Singleton
Ensures a class has only one instance and provides a global point of access to it.

```generic
class Singleton {
    private static instance: Singleton?

    private init() {}

    static func getInstance() -> Singleton {
        if instance == nil {
            instance = Singleton()
        }
        return instance!
    }
}
```

## 2. Factory Method
Defines an interface for creating an object, but lets subclasses alter the type of objects that will be created.

```generic
abstract class Product {
    // Product code
}

class ConcreteProduct: Product {
    // ConcreteProduct code
}

abstract class Creator {
    abstract func factoryMethod() -> Product

    func someOperation() {
        let product = factoryMethod()
        // Use the product
    }
}

class ConcreteCreator: Creator {
    override func factoryMethod() -> Product {
        return ConcreteProduct()
    }
}
```

## 3. Abstract Factory
Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

```generic
interface AbstractFactory {
    func createProductA() -> ProductA
    func createProductB() -> ProductB
}

class ConcreteFactory1: AbstractFactory {
    func createProductA() -> ProductA {
        return ProductA1()
    }
    func createProductB() -> ProductB {
        return ProductB1()
    }
}

class ConcreteFactory2: AbstractFactory {
    func createProductA() -> ProductA {
        return ProductA2()
    }
    func createProductB() -> ProductB {
        return ProductB2()
    }
}
```

## 4. Builder
Separates the construction of a complex object from its representation, allowing the same construction process to create different representations.

```generic
class Product {
    var partA: String?
    var partB: String?

    func setPartA(partA: String) {
        self.partA = partA
    }

    func setPartB(partB: String) {
        self.partB = partB
    }
}

abstract class Builder {
    protected var product = Product()

    abstract func buildPartA()
    abstract func buildPartB()

    func getResult() -> Product {
        return product
    }
}

class ConcreteBuilder: Builder {
    override func buildPartA() {
        product.setPartA(partA: "Part A")
    }

    override func buildPartB() {
        product.setPartB(partB: "Part B")
    }
}

class Director {
    private var builder: Builder?

    func setBuilder(builder: Builder) {
        self.builder = builder
    }

    func construct() -> Product {
        builder?.buildPartA()
        builder?.buildPartB()
        return builder!.getResult()
    }
}
```

## 5. Prototype
Creates new objects by copying an existing object, known as the prototype.

```generic
abstract class Prototype {
    func clone() -> Prototype {
        return self.copy() as! Prototype
    }
}

class ConcretePrototype: Prototype {
    var field: String?

    func setField(field: String) {
        self.field = field
    }

    func getField() -> String? {
        return field
    }
}
```

These patterns provide various ways to create objects, each with its own advantages and use cases, helping to make the design more flexible and reusable.