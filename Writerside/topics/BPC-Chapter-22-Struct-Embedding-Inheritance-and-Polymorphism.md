# Chapter 22 - Struct Embedding, Inheritance, and Polymorphism

In programming, struct embedding, inheritance, and polymorphism are foundational concepts, especially in object-oriented and composite-oriented paradigms. They play a crucial role in structuring code for reusability, maintainability, and scalability. This guide explores these concepts in depth, explaining what they are and how they can be applied effectively across multiple languages like Python, PHP, Go, C++, and Zig.

## What Are Struct Embedding, Inheritance, and Polymorphism?

### Struct Embedding: Composition Over Inheritance
Struct embedding is a mechanism where one struct or class contains another struct or class as a member. It is commonly used in composite-oriented programming to achieve code reuse without relying on inheritance. Unlike inheritance, struct embedding explicitly expresses "has-a" relationships rather than "is-a" relationships. This approach is favored in languages like Go and Zig, which do not have classical inheritance.

### Inheritance: Establishing an "Is-A" Relationship
Inheritance is a cornerstone of object-oriented programming (OOP) that allows a class or struct to derive properties and behaviors from a parent (or base) class. This mechanism is used to model "is-a" relationships. For example, a `Car` class might inherit from a `Vehicle` class because a car "is a" vehicle. Inheritance facilitates code reuse, but it can introduce tight coupling if not used carefully.

### Polymorphism: One Interface, Multiple Implementations
Polymorphism is the ability of different types to be treated as instances of the same base type. This concept is closely tied to inheritance and interfaces. Polymorphism enables dynamic behavior where objects of different classes can be used interchangeably if they share a common interface or base class.

## The Role of Struct Embedding in Composite-Oriented Design

### Struct Embedding Basics in Go
Go supports struct embedding to achieve code reuse and composition without traditional inheritance. An embedded struct's fields and methods can be accessed as if they were part of the outer struct.

**Example in Go:**
```go
package main

import "fmt"

// Embedded struct
type Engine struct {
    HorsePower int
}

// Outer struct
type Car struct {
    Engine
    Brand string
}

func main() {
    car := Car{
        Engine: Engine{HorsePower: 300},
        Brand:  "Toyota",
    }
    fmt.Println(car.Brand)       // Output: Toyota
    fmt.Println(car.HorsePower) // Access embedded struct field
}
```

### Struct Embedding in Zig
Zig follows a similar approach to Go, emphasizing composition over inheritance.

**Example in Zig:**
```zig
const std = @import("std");

const Engine = struct {
    horsePower: u32,
};

const Car = struct {
    engine: Engine,
    brand: []const u8,
};

pub fn main() void {
    var car = Car{
        .engine = .{ .horsePower = 300 },
        .brand = "Toyota",
    };
    std.debug.print("Brand: {}, Horsepower: {}\n", .{car.brand, car.engine.horsePower});
}
```

## Inheritance for Modeling "Is-A" Relationships

### How Inheritance Works in C++
C++ supports inheritance, allowing derived classes to inherit members from a base class.

**Example in C++:**
```cpp
#include <iostream>
#include <string>
using namespace std;

class Vehicle {
public:
    string brand;
    void honk() {
        cout << "Honking!" << endl;
    }
};

class Car : public Vehicle {
public:
    int horsePower;
};

int main() {
    Car myCar;
    myCar.brand = "Toyota";
    myCar.horsePower = 300;
    cout << "Brand: " << myCar.brand << ", Horsepower: " << myCar.horsePower << endl;
    myCar.honk(); // Inherited method
    return 0;
}
```

### Using Inheritance in PHP
PHP implements inheritance through classes and supports overriding methods for polymorphic behavior.

**Example in PHP:**
```php
<?php
class Vehicle {
    public $brand;

    public function honk() {
        echo "Honking!\n";
    }
}

class Car extends Vehicle {
    public $horsePower;
}

$myCar = new Car();
$myCar->brand = "Toyota";
$myCar->horsePower = 300;
echo "Brand: {$myCar->brand}, Horsepower: {$myCar->horsePower}\n";
$myCar->honk(); // Inherited method
?>
```

## Polymorphism and Its Practical Applications

### Runtime Polymorphism in Python
Python's duck typing enables polymorphism without explicitly defining an interface or inheritance.

**Example in Python:**
```python
class Vehicle:
    def honk(self):
        print("Vehicle honking!")

class Car(Vehicle):
    def honk(self):
        print("Car honking!")

def make_it_honk(vehicle):
    vehicle.honk()

# Polymorphism in action
v = Vehicle()
c = Car()
make_it_honk(v)
make_it_honk(c)
```

### Interfaces and Polymorphism in Go
Go uses interfaces to implement polymorphism without inheritance.

**Example in Go:**
```go
package main

import "fmt"

type Honker interface {
    Honk()
}

type Vehicle struct{}
func (v Vehicle) Honk() {
    fmt.Println("Vehicle honking!")
}

type Car struct{}
func (c Car) Honk() {
    fmt.Println("Car honking!")
}

func makeItHonk(h Honker) {
    h.Honk()
}

func main() {
    v := Vehicle{}
    c := Car{}
    makeItHonk(v)
    makeItHonk(c)
}
```

### Achieving Polymorphism in Zig
Zig uses function pointers and tagged unions for polymorphism.

**Example in Zig:**
```zig
const std = @import("std");

const Honker = union(enum) {
    Vehicle,
    Car,
};

fn honk(h: Honker) void {
    switch (h) {
        .Vehicle => std.debug.print("Vehicle honking!\n", .{}),
        .Car => std.debug.print("Car honking!\n", .{}),
    }
}

pub fn main() void {
    honk(.Vehicle);
    honk(.Car);
}
```

## Comparing Struct Embedding, Inheritance, and Polymorphism

- **Struct Embedding** is most suitable when building modular, composable systems. It avoids tight coupling and is language-agnostic.
- **Inheritance** is a powerful tool for reusability but can introduce rigidity and tight coupling.
- **Polymorphism** provides flexibility, especially in dynamic systems, enabling interchangeable behaviors.

## When to Use Each Concept
- **Use struct embedding** when you need to reuse functionality without implying a strict hierarchical relationship.
- **Use inheritance** for "is-a" relationships where a derived type logically extends a base type.
- **Use polymorphism** to achieve flexible and dynamic behavior, especially when designing systems that rely on interchangeable components.

## Conclusion

Struct embedding, inheritance, and polymorphism are versatile tools that cater to different programming paradigms and design goals. By understanding these concepts and their use cases, developers can create more maintainable, modular, and scalable software. Whether you're working with Python, PHP, Go, C++, or Zig, these principles provide a robust foundation for effective programming.