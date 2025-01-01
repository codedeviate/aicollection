# Generics

Go added support for **generics** (also known as type parameters) in version 1.18, allowing you to write functions and data structures that can work with multiple types while providing compile-time type safety. Generics eliminate the need to rely on interfaces or duplicated code for common patterns. Below is an in-depth look at how generics work in Go, accompanied by examples demonstrating their usage and constraints.

---

## 1. Basic Concepts of Generics in Go

1. **Type Parameters**
    - Go allows functions, methods, and types (e.g., structs) to have type parameters in square brackets `[ ]`.
    - Example: `func Foo[T any](param T) { ... }`.

2. **Constraints**
    - A type parameter must satisfy a constraint, which specifies what operations or underlying types are permitted.
    - Common constraints are found in the `constraints` package, for example `constraints.Ordered` (for types supporting `<`, `>` comparisons).

3. **`any` Keyword**
    - `any` is a predeclared identifier that means “no constraint” (equivalent to `interface{}`).

4. **Compile-Time Type Safety**
    - Generic code is checked at compile time, ensuring that operations on type parameters are valid for the provided constraints.

---

## 2. Generic Functions

A generic function in Go has one or more type parameters in square brackets. For example:

### Example 1: A Generic `Min` Function

```go
package main

import (
	"fmt"

	"golang.org/x/exp/constraints" // requires "go get golang.org/x/exp/constraints"
)

// Min returns the smaller of two values.
// T must be ordered (i.e., supports < or > comparisons).
func Min[T constraints.Ordered](a, b T) T {
	if a < b {
		return a
	}
	return b
}

func main() {
	fmt.Println(Min(3, 5))         // int
	fmt.Println(Min(4.2, 2.1))     // float64
	fmt.Println(Min("apple", "z")) // string
}
```

**Explanation**:
- The function `Min[T constraints.Ordered]` declares a type parameter `T` constrained by `constraints.Ordered`.
- This means `T` can be any type that supports `<` and `>` (e.g., all numeric types, strings).
- The function can be called with `int`, `float64`, `string`, etc.

---

### Example 2: A Generic Slice Filter Function

```go
package main

import "fmt"

// Filter returns a new slice containing all elements from 's' for which 'keep' returns true.
func Filter[T any](s []T, keep func(T) bool) []T {
	var result []T
	for _, v := range s {
		if keep(v) {
			result = append(result, v)
		}
	}
	return result
}

func main() {
	nums := []int{1, 2, 3, 4, 5}
	isEven := func(n int) bool { return n%2 == 0 }

	evenNums := Filter(nums, isEven)
	fmt.Println(evenNums) // [2 4]

	strs := []string{"apple", "banana", "cherry"}
	hasFiveLetters := func(s string) bool { return len(s) == 5 }
	fiveLetterStrs := Filter(strs, hasFiveLetters)
	fmt.Println(fiveLetterStrs) // ["apple"]
}
```

**Explanation**:
- `Filter[T any]` accepts a slice of type `T` and a function that checks if an element should be kept.
- We can call `Filter` with slices of `int` and `string` without duplicating code.

---

## 3. Generic Types

You can also define structs or other composite types with type parameters, making them reusable for multiple underlying types.

### Example 3: A Generic Pair Type

```go
package main

import "fmt"

// Pair holds two values of possibly different types.
type Pair[A, B any] struct {
	First  A
	Second B
}

func main() {
	intString := Pair[int, string]{First: 10, Second: "hello"}
	fmt.Println(intString.First, intString.Second) // 10 hello

	stringFloat := Pair[string, float64]{First: "pi", Second: 3.14159}
	fmt.Println(stringFloat.First, stringFloat.Second) // pi 3.14159
}
```

**Explanation**:
- `Pair[A, B any]` defines two type parameters, `A` and `B`, each constrained by `any`.
- This allows storing different types in the same data structure without sacrificing type safety.

---

### Example 4: A Generic Stack

```go
package main

import "fmt"

// Stack is a LIFO data structure for elements of type T.
type Stack[T any] struct {
	data []T
}

// Push adds an element to the top of the stack.
func (s *Stack[T]) Push(v T) {
	s.data = append(s.data, v)
}

// Pop removes the top element of the stack.
func (s *Stack[T]) Pop() (T, bool) {
	if len(s.data) == 0 {
		var zero T
		return zero, false
	}
	index := len(s.data) - 1
	elem := s.data[index]
	s.data = s.data[:index]
	return elem, true
}

func main() {
	intStack := Stack[int]{}
	intStack.Push(10)
	intStack.Push(20)
	val, ok := intStack.Pop()
	fmt.Println(val, ok) // 20 true

	stringStack := Stack[string]{}
	stringStack.Push("go")
	stringStack.Push("generics")
	v, ok := stringStack.Pop()
	fmt.Println(v, ok) // generics true
}
```

**Explanation**:
- `Stack[T any]` is a generic type that stores elements of type `T`.
- Methods like `Push` and `Pop` operate on the stack with a known type `T`.
- This eliminates the need for interface-based stacks or code duplication.

---

## 4. Multiple Constraints

Constraints can also combine interfaces or types.

### Example 5: A Generic `Add` Function with Numeric Constraints

```go
package main

import (
	"fmt"

	"golang.org/x/exp/constraints"
)

// Numeric is a custom constraint satisfied by integer and float types.
type Numeric interface {
	constraints.Integer | constraints.Float
}

// Add sums two numeric values.
func Add[T Numeric](a, b T) T {
	return a + b
}

func main() {
	fmt.Println(Add[int](2, 3))         // 5
	fmt.Println(Add[float64](3.14, 2.71)) // 5.85
}
```

**Explanation**:
- `type Numeric` is defined as a union of `constraints.Integer` and `constraints.Float`.
- `Add[T Numeric]` can be used with either an integer or a floating-point type.

---

## 5. Using Type Inference

When calling generic functions, Go can often infer the type parameter from the arguments.

### Example 6: Type Inference

```go
package main

import (
	"fmt"

	"golang.org/x/exp/constraints"
)

func Multiply[T constraints.Integer | constraints.Float](a, b T) T {
	return a * b
}

func main() {
	// Type inference from arguments; no need to explicitly specify [int] or [float64].
	fmt.Println(Multiply(3, 4))       // infers T = int
	fmt.Println(Multiply(2.5, 1.5))   // infers T = float64
}
```

**Explanation**:
- We didn’t explicitly write `Multiply[int]` or `Multiply[float64]`; the compiler deduced type from the arguments.

---

## 6. Generics and Methods

Methods on a generic type can also have type parameters, though typically they share the same parameter as the type.

### Example 7: Generic Method on a Generic Type

```go
package main

import (
	"fmt"
	"golang.org/x/exp/constraints"
)

type NumberList[T constraints.Ordered] struct {
	values []T
}

// NewNumberList is a generic constructor
func NewNumberList[T constraints.Ordered](vals ...T) NumberList[T] {
	return NumberList[T]{values: vals}
}

// Max is a method that returns the largest value
func (nl NumberList[T]) Max() T {
	if len(nl.values) == 0 {
		var zero T
		return zero
	}
	maxVal := nl.values[0]
	for _, v := range nl.values[1:] {
		if v > maxVal {
			maxVal = v
		}
	}
	return maxVal
}

func main() {
	intList := NewNumberList(1, 5, 3, 9, 2)
	fmt.Println(intList.Max()) // 9

	floatList := NewNumberList(3.1, 2.4, 5.9)
	fmt.Println(floatList.Max()) // 5.9
}
```

**Explanation**:
- `NumberList[T constraints.Ordered]` restricts `T` to ordered types.
- The method `Max()` compares elements with `>`, which is valid under `constraints.Ordered`.

---

## 7. Constraints from Regular Interfaces

You can use any interface as a constraint, not just those from `constraints`. The key is that all required methods or operators must be supported at compile time. However, note that normal interfaces don’t let you specify operators like `<` or `+`; you’d rely on interface methods instead.

### Example 8: Custom Interface Constraint

```go
package main

import "fmt"

// Stringer is a standard interface from fmt.
type Stringer interface {
	String() string
}

// PrintStrings prints the string representation of any type that implements Stringer.
func PrintStrings[T Stringer](items []T) {
	for _, item := range items {
		fmt.Println(item.String())
	}
}

// Example type implementing Stringer
type User struct {
	Name string
}

func (u User) String() string {
	return "User: " + u.Name
}

func main() {
	users := []User{{Name: "Alice"}, {Name: "Bob"}}
	PrintStrings(users)
}
```

**Explanation**:
- `PrintStrings[T Stringer]` can only be used with types that have a `String()` method.
- The `User` type satisfies this requirement.

---

## 8. Potential Pitfalls and Limitations

1. **No Runtime Polymorphism**
    - Generics do not replace interfaces when you need dynamic dispatch or runtime polymorphism. Generics are resolved at compile time.

2. **Cannot Use Operators Arbitrarily**
    - You must define constraints if you want to use operators like `<`, `+`, or `==`. Go doesn’t automatically allow them for any type.

3. **Exporting Generic Types**
    - When you export a generic type or function, ensure the constraints are also publicly accessible if they are custom constraints.

4. **Complexity**
    - Overusing generics can make code more complex. Evaluate if a simpler approach (like just one or two specialized functions) might be more readable.

---

## Summary and Best Practices

- **Generics** in Go let you write reusable, type-safe code without duplicating functions for each type.
- **Constraints** define what operations or interfaces the type parameter must support.
- **Use generics** when you have truly type-agnostic logic (e.g., a data structure, an algorithm that operates on multiple types).
- **Don’t overuse** generics for simple tasks or where interfaces would suffice.
- **Profile readability**: A generic approach should be clearer than multiple specialized functions if your logic is truly the same for all types involved.

By understanding how to declare type parameters, apply constraints, and exploit type inference, you can harness Go’s generics to create versatile and maintainable code. As with any powerful feature, use it judiciously to ensure your code remains simple, efficient, and clear.