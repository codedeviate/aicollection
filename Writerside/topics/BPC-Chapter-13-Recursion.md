# Chapter 13 - Recursion

Recursion is a fundamental concept in programming that involves a function calling itself to solve a problem. This approach is particularly useful for problems that can be broken down into smaller, similar sub-problems. Recursion can be an elegant and powerful tool but requires a solid understanding to use effectively.

There are two main types of recursion:

1. **Direct Recursion**: This occurs when a function directly calls itself. For example, a function calculating the factorial of a number by calling itself is a case of direct recursion.

2. **Indirect Recursion**: This occurs when a function calls another function, which eventually calls the original function. For example, function `A` calls function `B`, and then `B` calls `A`.

Both types of recursion can be used to solve a variety of problems. However, each requires careful design to avoid issues such as infinite loops or excessive memory usage.

## How Recursion Works

At its core, recursion works by dividing a problem into two parts:

1. **Base Case**: This is the condition that stops the recursion. Without a base case, the recursion would continue indefinitely, leading to a stack overflow error.

2. **Recursive Case**: This is the part of the function where it calls itself with a smaller or simpler input, gradually working toward the base case.

## Examples of Recursive Functions

### Factorial Calculation

The factorial of a number (n!) is the product of all positive integers from 1 to n. Here’s how you can compute it using recursion:

**Python:**
```python
def factorial(n):
    if n == 0:
        return 1  # Base case
    return n * factorial(n - 1)  # Recursive case

print(factorial(5))  # Output: 120
```

**PHP:**
```php
function factorial($n) {
    if ($n == 0) {
        return 1; // Base case
    }
    return $n * factorial($n - 1); // Recursive case
}

echo factorial(5); // Output: 120
```

**Go:**
```go
package main

import "fmt"

func factorial(n int) int {
    if n == 0 {
        return 1 // Base case
    }
    return n * factorial(n-1) // Recursive case
}

func main() {
    fmt.Println(factorial(5)) // Output: 120
}
```

**C++:**
```cpp
#include <iostream>
using namespace std;

int factorial(int n) {
    if (n == 0) {
        return 1; // Base case
    }
    return n * factorial(n - 1); // Recursive case
}

int main() {
    cout << factorial(5) << endl; // Output: 120
    return 0;
}
```

**Zig:**
```zig
const std = @import("std");

fn factorial(n: u64) u64 {
    if (n == 0) {
        return 1; // Base case
    }
    return n * factorial(n - 1); // Recursive case
}

pub fn main() void {
    std.debug.print("{d}\n", .{factorial(5)}); // Output: 120
}
```

## Tail Recursion for Optimized Performance

Tail recursion is a specific form of recursion where the recursive call is the last operation in the function. This allows some compilers or interpreters to optimize the function and reuse the current stack frame, reducing memory usage.

### Tail Recursive Factorial

**Python:**
```python
def tail_factorial(n, accumulator=1):
    if n == 0:
        return accumulator  # Base case
    return tail_factorial(n - 1, accumulator * n)  # Recursive case

print(tail_factorial(5))  # Output: 120
```

## Common Use Cases of Recursion

### Traversing Data Structures

Recursion is often used for traversing hierarchical data structures like trees and graphs.

**Example: Depth-First Search (DFS) in Python**
```python
def dfs(graph, node, visited):
    if node not in visited:
        visited.add(node)
        print(node)
        for neighbor in graph[node]:
            dfs(graph, neighbor, visited)

# Example graph
graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': [],
    'F': []
}
dfs(graph, 'A', set())
```

### Solving Divide and Conquer Problems

Algorithms like merge sort, quicksort, and binary search rely on recursion to divide problems into smaller sub-problems.

**Example: Merge Sort in Python**
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    return merge(left, right)

def merge(left, right):
    sorted_list = []
    while left and right:
        if left[0] < right[0]:
            sorted_list.append(left.pop(0))
        else:
            sorted_list.append(right.pop(0))
    sorted_list.extend(left or right)
    return sorted_list

print(merge_sort([5, 3, 8, 4, 2]))  # Output: [2, 3, 4, 5, 8]
```

## Pitfalls of Recursion

- **Stack Overflow**: Occurs when recursion depth exceeds the stack limit.
- **Performance Overhead**: Recursion can be less efficient than iteration due to repeated function calls and memory use.
- **Debugging Difficulty**: Recursive functions can be harder to trace and debug compared to iterative solutions.

## Summary

Recursion is a versatile and powerful tool in programming, enabling elegant solutions for many complex problems. By understanding the principles of base cases, recursive cases, and optimization techniques like tail recursion, you can effectively leverage recursion in your code. However, it’s crucial to recognize its limitations and use it judiciously to avoid performance bottlenecks and errors.

