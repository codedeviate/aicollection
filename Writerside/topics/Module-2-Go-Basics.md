# Module 2: Go Basics

## Detailed Topics:

### Syntax and Constructs
Go offers a straightforward syntax that emphasizes readability. Key elements include:
- **Variable Declaration**:
    - Declare variables using `var` or shorthand `:=`.
  ```go
  var x int = 10
  y := 20
  ```
- **Constants**:
    - Use `const` to define immutable values.
  ```go
  const Pi = 3.14
  ```
- **Functions**:
    - Define reusable code blocks.
  ```go
  func add(a int, b int) int {
      return a + b
  }
  ```

### Data Types and Collections
1. **Slices**:
    - Dynamic arrays that adjust size as needed.
   ```go
   numbers := []int{1, 2, 3, 4}
   numbers = append(numbers, 5)
   ```
2. **Maps**:
    - Key-value data structures for fast lookups.
   ```go
   scores := map[string]int{"Alice": 90, "Bob": 85}
   fmt.Println(scores["Alice"])
   ```

### Control Structures
1. **Conditional Statements**:
   ```go
   if x > 0 {
       fmt.Println("Positive")
   } else {
       fmt.Println("Non-positive")
   }
   ```
2. **For-Loops**:
   ```go
   for i := 0; i < 5; i++ {
       fmt.Println(i)
   }
   ```
3. **Switch Cases**:
   ```go
   switch day := "Monday"; day {
   case "Monday":
       fmt.Println("Start of the week")
   default:
       fmt.Println("Another day")
   }
   ```

## Detailed Hands-On

### Practice Slicing Arrays and Iterating Over Maps
1. **Slice Manipulation**:
   ```go
   fruits := []string{"apple", "banana", "cherry"}
   fmt.Println(fruits[1:])
   ```
2. **Map Iteration**:
   ```go
   capitals := map[string]string{"France": "Paris", "Italy": "Rome"}
   for country, capital := range capitals {
       fmt.Printf("%s: %s\n", country, capital)
   }
   ```

### Create a Recursive and Iterative Function to Compute Factorials
1. **Recursive Factorial**:
   ```go
   func factorialRecursive(n int) int {
       if n == 0 {
           return 1
       }
       return n * factorialRecursive(n-1)
   }
   ```
2. **Iterative Factorial**:
   ```go
   func factorialIterative(n int) int {
       result := 1
       for i := 1; i <= n; i++ {
           result *= i
       }
       return result
   }
   ```

