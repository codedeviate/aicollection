# Chapter 12 - Closures

Closures are a fundamental concept in programming, particularly in languages that support first-class functions. A closure is essentially a function that "remembers" the environment in which it was created. This allows the function to access variables from its enclosing scope even after that scope has exited.

Closures provide powerful mechanisms for managing state, encapsulation, and callbacks. They are prevalent in functional programming paradigms and are often used to handle asynchronous tasks, event listeners, or partial function application.

## Different Types of Closures: A Brief Overview

Closures can manifest in various ways depending on how they capture and manage their surrounding state. Here are some distinct types:

1. **Anonymous Function Closures**: These are unnamed functions that capture their environment.
2. **Named Function Closures**: These are named functions that maintain references to variables outside their scope.
3. **Lexical Closures**: Functions that rely on variables defined in their lexical (static) scope.
4. **Persistent Closures**: Closures that maintain their state across multiple calls, often used to manage persistent data or counters.

Let’s dive deeper into the concept and explore their applications with examples in Python, PHP, Go, C++, and Zig.

---

## What Makes Closures Unique?

Closures are distinct because they "close over" their surrounding scope, enabling the function to maintain access to variables outside their immediate block. This is particularly useful for:

- **Encapsulation**: Encapsulating private state within a function.
- **Callbacks**: Passing functions as arguments with preserved context.
- **Partial Application**: Predefining part of a function's arguments while keeping the rest dynamic.
- **State Management**: Retaining state between function calls without using global variables.

---

## Understanding Closures Through Examples in Python

In Python, closures are often used due to its support for nested functions.

## Example 1: Capturing Variables from Outer Scope

```python
def outer_function(x):
    def inner_function(y):
        return x + y
    return inner_function

add_five = outer_function(5)
print(add_five(10))  # Output: 15
```

The `inner_function` captures the variable `x` from the `outer_function`.

## Example 2: Persistent State with Closures

```python
def counter():
    count = 0

    def increment():
        nonlocal count
        count += 1
        return count

    return increment

counter_instance = counter()
print(counter_instance())  # Output: 1
print(counter_instance())  # Output: 2
```

The `increment` function persists the value of `count` using the `nonlocal` keyword.

---

## Closures in PHP: An Object-Oriented Perspective

PHP supports closures through its `Closure` class, and you can explicitly bind variables to closures.

## Example 1: Simple Closure Capturing Outer Variables

```php
function createAdder($x) {
    return function ($y) use ($x) {
        return $x + $y;
    };
}

$addFive = createAdder(5);
echo $addFive(10); // Output: 15
```

The `use` keyword is used to import variables into the closure’s scope.

## Example 2: Stateful Closures

```php
function counter() {
    $count = 0;
    return function () use (&$count) {
        $count++;
        return $count;
    };
}

$counterInstance = counter();
echo $counterInstance(); // Output: 1
echo $counterInstance(); // Output: 2
```

The `&` symbol allows the closure to modify the external variable directly.

---

## Practical Closures in Go: Functions as First-Class Citizens

Go supports closures with its function literals.

## Example 1: Using Closures to Capture State

```go
package main

import "fmt"

func main() {
    adder := func(x int) func(int) int {
        return func(y int) int {
            return x + y
        }
    }

    addFive := adder(5)
    fmt.Println(addFive(10)) // Output: 15
}
```

## Example 2: Stateful Closure

```go
package main

import "fmt"

func counter() func() int {
    count := 0
    return func() int {
        count++
        return count
    }
}

func main() {
    countInstance := counter()
    fmt.Println(countInstance()) // Output: 1
    fmt.Println(countInstance()) // Output: 2
}
```

---

## Closures in C++: Lambda Expressions and Captures

C++ supports closures through lambda expressions with various capture modes.

## Example 1: Capturing Variables by Value

```cpp
#include <iostream>
#include <functional>

int main() {
    int x = 5;
    auto add = [x](int y) {
        return x + y;
    };

    std::cout << add(10) << std::endl; // Output: 15
    return 0;
}
```

## Example 2: Capturing by Reference for Statefulness

```cpp
#include <iostream>

int main() {
    int count = 0;
    auto counter = [&count]() {
        return ++count;
    };

    std::cout << counter() << std::endl; // Output: 1
    std::cout << counter() << std::endl; // Output: 2
    return 0;
}
```

---

## Exploring Closures in Zig: Minimalism with Captures

In Zig, closures can be achieved using inline function captures.

## Example 1: Passing Captured Variables

```zig
const std = @import("std");

fn createAdder(x: i32) fn (i32) i32 {
    return (fn (y: i32) i32 {
        return x + y;
    });
}

pub fn main() void {
    const addFive = createAdder(5);
    std.debug.print("{}\n", .{addFive(10)}); // Output: 15
}
```

## Example 2: Stateful Closures Using Structs

```zig
const std = @import("std");

const Counter = struct {
    count: i32,
    pub fn increment(self: *Counter) i32 {
        self.count += 1;
        return self.count;
    }
};

pub fn main() void {
    var counter = Counter{ .count = 0 };
    std.debug.print("{}\n", .{counter.increment()}); // Output: 1
    std.debug.print("{}\n", .{counter.increment()}); // Output: 2
}
```

---

## Real-World Applications of Closures

Closures have numerous practical uses across programming:

1. **Event Handling**: Assigning context-aware callbacks.
2. **Functional Programming**: Higher-order functions like `map`, `filter`, and `reduce`.
3. **Data Encapsulation**: Keeping data private within a function.
4. **Partial Application**: Preconfiguring functions with default arguments.
5. **Asynchronous Operations**: Maintaining context in asynchronous code.

---

## Conclusion: Harnessing the Power of Closures

Closures are a versatile tool that empower developers to write more expressive, concise, and maintainable code. By capturing variables from their surrounding environment, closures enable encapsulation, state management, and functional programming paradigms. Understanding closures deeply across various languages equips developers to solve complex problems elegantly.