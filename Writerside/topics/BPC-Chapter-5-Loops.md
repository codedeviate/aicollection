# Chapter 5 - Loop Types

In programming, loops are a fundamental construct used to repeat a block of code multiple times, either for a fixed number of iterations or while a specific condition holds true. Loops are essential for automating repetitive tasks, iterating over collections of data, and implementing algorithms that require repeated processing. By reducing the need for manual repetition, loops help improve code efficiency, readability, and maintainability.

Below is a concise description of the loop types available in Python, PHP, C++, Zig, and Go.

---

## Python
Python provides three primary types of loops:

1. **`for` Loop**:
   - Iterates over a sequence (like a list, tuple, string, or range).
   - Example:
     ```python
     for i in range(5):
         print(i)
     ```

2. **`while` Loop**:
   - Continues execution as long as a given condition is `True`.
   - Example:
     ```python
     i = 0
     while i < 5:
         print(i)
         i += 1
     ```

3. **Nested Loops**:
   - Loops within loops.
   - Example:
     ```python
     for i in range(3):
         for j in range(2):
             print(f"i: {i}, j: {j}")
     ```

Python also provides constructs like `break`, `continue`, and `else` (executed when the loop finishes without being interrupted by `break`).

---

## PHP
PHP supports several loop types:

1. **`for` Loop**:
   - Iterates using a counter.
   - Example:
     ```php
     for ($i = 0; $i < 5; $i++) {
         echo $i . "\n";
     }
     ```

2. **`while` Loop**:
   - Executes while a condition is `true`.
   - Example:
     ```php
     $i = 0;
     while ($i < 5) {
         echo $i . "\n";
         $i++;
     }
     ```

3. **`do-while` Loop**:
   - Executes the block at least once before checking the condition.
   - Example:
     ```php
     $i = 0;
     do {
         echo $i . "\n";
         $i++;
     } while ($i < 5);
     ```

4. **`foreach` Loop**:
   - Iterates over arrays or objects.
   - Example:
     ```php
     $arr = ["a", "b", "c"];
     foreach ($arr as $value) {
         echo $value . "\n";
     }
     ```

PHP also provides `break` and `continue` for controlling loop flow.

---

## C++
C++ offers a range of looping constructs:

1. **`for` Loop**:
   - Standard counter-based iteration.
   - Example:
     ```cpp
     for (int i = 0; i < 5; i++) {
         std::cout << i << std::endl;
     }
     ```

2. **`while` Loop**:
   - Repeats while a condition is true.
   - Example:
     ```cpp
     int i = 0;
     while (i < 5) {
         std::cout << i << std::endl;
         i++;
     }
     ```

3. **`do-while` Loop**:
   - Executes at least once.
   - Example:
     ```cpp
     int i = 0;
     do {
         std::cout << i << std::endl;
         i++;
     } while (i < 5);
     ```

4. **Range-Based `for` Loop**:
   - Simplified iteration over containers (introduced in C++11).
   - Example:
     ```cpp
     std::vector<int> nums = {1, 2, 3};
     for (int num : nums) {
         std::cout << num << std::endl;
     }
     ```

5. **Nested Loops**:
   - Loops inside loops.
   - Example:
     ```cpp
     for (int i = 0; i < 3; i++) {
         for (int j = 0; j < 2; j++) {
             std::cout << "i: " << i << ", j: " << j << std::endl;
         }
     }
     ```

C++ also supports `break` and `continue` for loop control.

---

## Zig
Zig offers loops with a slightly different syntax and approach:

1. **`while` Loop**:
   - Executes as long as a condition is true.
   - Example:
     ```zig
     var i: i32 = 0;
     while (i < 5) : (i += 1) {
         std.debug.print("{d}\n", .{i});
     }
     ```

2. **`for` Loop**:
   - Iterates over collections or ranges.
   - Example:
     ```zig
     const items = [_]i32{1, 2, 3};
     for (items) |item| {
         std.debug.print("{d}\n", .{item});
     }
     ```

3. **`inline for` Loop**:
   - Compact loop syntax often used in compile-time or single expressions.
   - Example:
     ```zig
     inline for (std.range(0, 5)) |i| {
         std.debug.print("{d}\n", .{i});
     }
     ```

4. **Labeled Loops**:
   - Supports labeling for breaking out of nested loops.
   - Example:
     ```zig
     var i: i32 = 0;
     outer: while (i < 5) : (i += 1) {
         if (i == 3) break :outer;
         std.debug.print("{d}\n", .{i});
     }
     ```

---

## Go
Go provides several looping constructs, primarily centered around the `for` loop, which can be adapted to cover the functionality of other common loop types. Go does not have a `while` or `do-while` loop, but these can be implemented using `for`.

1. **`for` Loop**:
   - The standard `for` loop in Go is similar to other languages, with initialization, condition, and post-expression.
   - Example:
     ```go
     package main
     
     import "fmt"

     func main() {
         for i := 0; i < 5; i++ {
             fmt.Println(i)
         }
     }
     ```

2. **`while`-like Loop**:
   - Go uses the `for` loop without an initialization or post-expression to mimic a `while` loop.
   - Example:
     ```go
     package main
     
     import "fmt"

     func main() {
         i := 0
         for i < 5 {
             fmt.Println(i)
             i++
         }
     }
     ```

3. **Infinite Loop**:
   - Omitting all three components of the `for` loop results in an infinite loop.
   - Example:
     ```go
     package main
     
     import "fmt"

     func main() {
         i := 0
         for {
             if i >= 5 {
                 break
             }
             fmt.Println(i)
             i++
         }
     }
     ```

4. **Range-based `for` Loop**:
   - Iterates over elements of arrays, slices, maps, or strings.
   - Example:
     ```go
     package main
     
     import "fmt"

     func main() {
         nums := []int{1, 2, 3}
         for index, value := range nums {
             fmt.Printf("Index: %d, Value: %d\n", index, value)
         }
     }
     ```

Go also supports `break` and `continue` for controlling loop flow.

---

Each language offers flexibility and functionality through these loops, and understanding their syntax and applications is crucial for efficient programming.

