# Chapter 10 - Multiple Return Values

When working with functions, returning more than one value can simplify workflows and improve code organization. Multiple return values allow a single function to return multiple pieces of information at once, catering to scenarios like error handling, complex data decomposition, or combined results from related computations.

This guide explores how multiple return values can be implemented and used in different programming languages like Python, PHP, C++, Zig, and Go, along with practical examples.

---

## What Makes Multiple Return Values Useful?

Multiple return values are useful for encapsulating related data into a single function call. They allow functions to return:
- **Results with metadata** (e.g., a calculation result and its confidence score).
- **Error codes alongside results** for better error handling.
- **Intermediate and final calculations** simultaneously.

Languages offer varied support, from Python's tuples to C++ structs and Zig's native tuples. PHP achieves this using arrays, while Go provides direct multiple return value support. Each method has its strengths and is tailored to specific use cases.

---

## Leveraging Multiple Return Values in Python Functions

Python's built-in support for tuples makes returning multiple values effortless and intuitive.

### Example of Simple Multiple Results
```python
def calculate(a, b):
    return a + b, a * b

sum_result, product_result = calculate(4, 7)
print(f"Sum: {sum_result}, Product: {product_result}")
```

Here, the results are packed into a tuple, which is then unpacked into variables for further use.

### Advanced Python Use Case: Error Reporting
```python
def divide(a, b):
    if b == 0:
        return None, "Error: Division by zero"
    return a / b, None

result, error = divide(10, 0)
if error:
    print(error)
else:
    print(f"Result: {result}")
```

Python’s tuple unpacking makes this approach clean and concise.

---

## Using Associative Arrays for Multiple Values in PHP

PHP lacks native support for multiple return values but achieves this functionality through arrays.

### Example: Associative Arrays for Organized Results
```php
function calculate($a, $b) {
    return [
        "sum" => $a + $b,
        "product" => $a * $b
    ];
}

$results = calculate(4, 7);
echo "Sum: {$results['sum']}, Product: {$results['product']}";
```

Arrays act as containers for named return values, making it easy to retrieve and manage them.

### Error Handling Example in PHP
```php
function divide($a, $b) {
    if ($b == 0) {
        return ["result" => null, "error" => "Cannot divide by zero"];
    }
    return ["result" => $a / $b, "error" => null];
}

$output = divide(10, 0);
if ($output["error"]) {
    echo $output["error"];
} else {
    echo "Result: {$output['result']}";
}
```

This demonstrates combining error handling with functional results.

---

## Using Structs and Pairs in C++ for Returning Multiple Results

C++ supports multiple return values through features like `std::pair`, `std::tuple`, and custom structs.

### Example with `std::pair` for Simplified Results
```cpp
#include <iostream>
#include <utility>

std::pair<int, int> calculate(int a, int b) {
    return std::make_pair(a + b, a * b);
}

int main() {
    auto result = calculate(4, 7);
    std::cout << "Sum: " << result.first << ", Product: " << result.second << std::endl;
    return 0;
}
```

The `std::pair` is a lightweight way to return two values.

### Struct-Based Approach for Readability
```cpp
#include <iostream>

struct Results {
    int sum;
    int product;
};

Results calculate(int a, int b) {
    return {a + b, a * b};
}

int main() {
    Results result = calculate(4, 7);
    std::cout << "Sum: " << result.sum << ", Product: " << result.product << std::endl;
    return 0;
}
```

Using a struct gives descriptive names to each value, improving code clarity.

### Using Tuples for Complex Returns in C++
```cpp
#include <tuple>
#include <iostream>

std::tuple<int, int, bool> process(int a, int b) {
    return std::make_tuple(a + b, a * b, a > b);
}

int main() {
    auto [sum, product, comparison] = process(4, 7);
    std::cout << "Sum: " << sum << ", Product: " << product << ", A > B: " << std::boolalpha << comparison << std::endl;
    return 0;
}
```

Tuples offer flexibility for returning more than two values in C++.

---

## Working with Tuples for Multiple Outputs in Zig

Zig provides first-class support for multiple return values via tuples and error handling mechanisms.

### Simple Example of Returning Two Values
```zig
const std = @import("std");

fn calculate(a: i32, b: i32) (i32, i32) {
    return a + b, a * b;
}

pub fn main() void {
    const stdout = std.io.getStdOut().writer();
    const result = calculate(4, 7);
    stdout.print("Sum: {}, Product: {}\n", .{result});
}
```

### Error and Value Combined Return in Zig
```zig
const std = @import("std");

fn divide(a: i32, b: i32) !i32 {
    if (b == 0) return error.DivisionByZero;
    return a / b;
}

pub fn main() void {
    const stdout = std.io.getStdOut().writer();
    const result = divide(10, 0);
    switch (result) {
        error => stdout.print("Error: Division by zero\n", .{}),
        => stdout.print("Result: {}\n", .{}),
    }
}
```

Zig’s tuple syntax and error-handling mechanisms make this efficient and robust.

---

## Go’s Built-In Support for Multiple Return Values

Go natively supports multiple return values, making it straightforward and concise.

### Example: Returning Two Values
```go
package main

import "fmt"

func calculate(a, b int) (int, int) {
    return a + b, a * b
}

func main() {
    sum, product := calculate(4, 7)
    fmt.Printf("Sum: %d, Product: %d\n", sum, product)
}
```

Go makes it simple to return and unpack multiple results in one step.

### Error Handling with Multiple Returns
```go
package main

import "fmt"

func divide(a, b int) (int, error) {
    if b == 0 {
        return 0, fmt.Errorf("division by zero")
    }
    return a / b, nil
}

func main() {
    result, err := divide(10, 0)
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("Result:", result)
    }
}
```

Go elegantly combines error handling with multiple return values.

---

## Practical Scenarios for Multiple Return Values

### Common Use Cases:
1. **Error Reporting:** Combine results with error details for better error management.
2. **Complex Data Decomposition:** Split complex objects or datasets into meaningful components.
3. **Performance Optimization:** Save on function calls by returning all required data in one go.

### Advantages:
- Improves code clarity and organization.
- Facilitates error handling alongside primary results.
- Reduces redundant code and repetitive function calls.

---

## Conclusion: Mastering Multiple Return Values

Understanding multiple return values is essential for writing efficient and maintainable code. Different programming languages approach this feature uniquely, from Python's tuples and PHP's arrays to C++'s structs, Zig's native support, and Go's built-in mechanisms. By learning these techniques, you'll gain more flexibility and power in managing data flow in your programs.