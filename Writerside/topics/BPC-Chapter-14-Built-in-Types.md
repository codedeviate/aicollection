# Chapter 14 - Built-in Types

When working with programming languages, built-in types are among the foundational concepts that every programmer should grasp. Built-in types, also known as primitive or intrinsic types, are the data types provided directly by a programming language. These types are the building blocks for storing and manipulating data within a program. Unlike custom or user-defined types, built-in types come pre-packaged with the language and are optimized for performance and ease of use.

Different programming languages provide a set of built-in types, which typically include categories like numbers, text, booleans, and more. Each type serves a specific purpose and allows you to handle various forms of data effectively.

In this article, we'll explore the common categories of built-in types, delve into their unique properties, and demonstrate their usage with examples in **Python**, **PHP**, **Go**, **C++**, and **Zig**.

---

## Numeric Types: Handling Numbers Efficiently

Numeric types are used for representing numbers in various forms. They are typically categorized as integers, floating-point numbers, and sometimes special types like complex numbers.

### Integer Types

**Integers** store whole numbers and are commonly used for counting, indexing, and performing arithmetic operations. They do not contain a fractional component.

Examples:

- **Python**: `int` supports arbitrary precision.
- **PHP**: `int` stores signed integers.
- **Go**: `int`, `int8`, `int16`, `int32`, `int64`.
- **C++**: `int`, `long`, `short`.
- **Zig**: `i32`, `i64`, `u32`, `u64` (signed and unsigned integers).

#### Python Example
```python
x = 42
y = -10
print(x + y)  # Output: 32
```

#### PHP Example
```php
$x = 42;
$y = -10;
echo $x + $y; // Output: 32
```

#### Go Example
```go
package main
import "fmt"

func main() {
    var x int = 42
    var y int = -10
    fmt.Println(x + y)  // Output: 32
}
```

#### C++ Example
```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 42;
    int y = -10;
    cout << x + y << endl;  // Output: 32
    return 0;
}
```

#### Zig Example
```zig
const std = @import("std");

pub fn main() void {
    const x: i32 = 42;
    const y: i32 = -10;
    std.debug.print("{}\n", .{x + y}); // Output: 32
}
```

---

### Floating-point Types

**Floating-point numbers** represent real numbers and are used for calculations requiring decimal points, such as scientific computations and financial applications.

Examples:

- **Python**: `float` for double-precision floating-point numbers.
- **PHP**: `float` or `double`.
- **Go**: `float32`, `float64`.
- **C++**: `float`, `double`.
- **Zig**: `f32`, `f64`.

---

## Text Types: Managing Strings

Strings represent sequences of characters, commonly used for handling text.

### Python Strings
```python
greeting = "Hello, World!"
print(greeting.upper())  # Output: HELLO, WORLD!
```

### PHP Strings
```php
$greeting = "Hello, World!";
echo strtoupper($greeting);  // Output: HELLO, WORLD!
```

### Go Strings
```go
package main
import (
    "fmt"
    "strings"
)

func main() {
    greeting := "Hello, World!"
    fmt.Println(strings.ToUpper(greeting))  // Output: HELLO, WORLD!
}
```

### C++ Strings
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string greeting = "Hello, World!";
    transform(greeting.begin(), greeting.end(), greeting.begin(), ::toupper);
    cout << greeting << endl;  // Output: HELLO, WORLD!
    return 0;
}
```

### Zig Strings
```zig
const std = @import("std");

pub fn main() void {
    const greeting = "Hello, World!";
    std.debug.print("{}\n", .{greeting}); // Zig doesn't provide native string methods, external libraries may help.
}
```

---

## Boolean Types: Representing True or False

**Booleans** are used for logical operations and conditions. They take two values: `true` or `false`.

- **Python**: `True`, `False`.
- **PHP**: `true`, `false`.
- **Go**: `bool`.
- **C++**: `bool`.
- **Zig**: `bool`.

Examples:
```python
is_active = True
print(not is_active)  # Output: False
```

```php
$is_active = true;
echo !$is_active;  // Output: 
```

---

## Composite Types: Combining Data

Examples for arrays.

Continuing with composite types, here's a detailed look:

## Composite Types: Organizing Multiple Values

Composite types allow you to group multiple values together in structured formats. Common examples include arrays, lists, and dictionaries (also known as associative arrays or hash maps). These types are versatile and are often used to store collections of related data.

---

### Array Types: Storing Ordered Collections

An **array** is a collection of elements, often of the same type, stored in a contiguous block of memory. Arrays provide an efficient way to handle multiple values using indexed access.

#### Python Lists (Dynamic Arrays)
In Python, the `list` type is a dynamic array that can store elements of mixed types.
```python
numbers = [1, 2, 3, 4]
numbers.append(5)
print(numbers[0])  # Output: 1
```

#### PHP Arrays
PHP uses arrays as flexible structures that can act as ordered lists or associative arrays.
```php
$numbers = [1, 2, 3, 4];
$numbers[] = 5;
echo $numbers[0];  // Output: 1
```

#### Go Slices (Dynamic Arrays)
Go uses slices to represent dynamically sized arrays.
```go
package main
import "fmt"

func main() {
    numbers := []int{1, 2, 3, 4}
    numbers = append(numbers, 5)
    fmt.Println(numbers[0])  // Output: 1
}
```

#### C++ Arrays
C++ provides both fixed-size arrays and dynamic arrays through the Standard Template Library (STL).
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4};
    numbers.push_back(5);
    cout << numbers[0] << endl;  // Output: 1
    return 0;
}
```

#### Zig Arrays
Zig uses arrays with fixed or dynamic lengths.
```zig
const std = @import("std");

pub fn main() void {
    var numbers: [4]i32 = [_]i32{1, 2, 3, 4};
    std.debug.print("{}\n", .{numbers[0]}); // Output: 1
}
```

---

### Dictionaries or Maps: Key-Value Storage

Dictionaries (or maps) allow you to store data in a key-value format for efficient lookups.

#### Python Dictionaries
```python
user = {"name": "Alice", "age": 25}
print(user["name"])  # Output: Alice
```

#### PHP Associative Arrays
```php
$user = ["name" => "Alice", "age" => 25];
echo $user["name"];  // Output: Alice
```

#### Go Maps
```go
package main
import "fmt"

func main() {
    user := map[string]interface{}{"name": "Alice", "age": 25}
    fmt.Println(user["name"])  // Output: Alice
}
```

#### C++ Maps
```cpp
#include <iostream>
#include <map>
using namespace std;

int main() {
    map<string, int> user = {{"name", 0}, {"age", 25}};  // Example map
    cout << user["age"] << endl;  // Output: 25
    return 0;
}
```

#### Zig Dictionaries (Simulated)
Zig does not provide built-in dictionaries, but you can use libraries or implement custom key-value data structures.

---

## Special Types: Handling Edge Cases

Some built-in types are designed for specific use cases:

- **Python**: `None` represents the absence of a value.
- **PHP**: `null` serves a similar purpose.
- **Go**: `nil` is used for pointers, slices, maps, and channels.
- **C++**: `nullptr` is the null pointer.
- **Zig**: `null` can be used in optional types.

Examples:
```python
x = None
print(x is None)  # Output: True
```

```php
$x = null;
var_dump(is_null($x));  // Output: bool(true)
```

---

## Conclusion: Leveraging Built-in Types

Built-in types form the foundation of any programming language. Understanding these types allows you to efficiently store, manipulate, and retrieve data in your applications. By mastering these essential building blocks, you can write cleaner, more effective code across languages. Each language’s implementation of these types offers unique nuances, so exploring them thoroughly is key to developing a deeper understanding of programming fundamentals.