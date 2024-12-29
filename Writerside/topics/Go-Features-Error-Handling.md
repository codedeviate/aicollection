# Error Handling

Error handling in Go is explicit, simple, and straightforward, focusing on handling errors as part of the normal control flow. Go does not have exceptions like some other languages; instead, it uses **multiple return values** to return an error along with the result of a function. This approach promotes clear and explicit error management.

---

## Key Concepts of Error Handling in Go

1. **Error Type**:
    - Errors in Go are represented by the `error` interface from the `builtin` package:
      ```go
      type error interface {
          Error() string
      }
      ```
    - Any type that implements the `Error()` method satisfies the `error` interface.

2. **Returning Errors**:
    - Functions in Go often return an `error` as the second value:
      ```go
      func doSomething() (string, error)
      ```

3. **Error Checking**:
    - Errors are explicitly checked after calling a function.

4. **Custom Errors**:
    - Developers can define custom error types for more detailed error handling.

5. **Error Wrapping**:
    - Go 1.13 introduced error wrapping to provide additional context for errors using `errors` and `fmt` packages.

---

## Examples of Error Handling

### Example 1: Basic Error Handling
```go
package main

import (
	"errors"
	"fmt"
)

func divide(a, b int) (int, error) {
	if b == 0 {
		return 0, errors.New("division by zero")
	}
	return a / b, nil
}

func main() {
	result, err := divide(10, 0)
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	fmt.Println("Result:", result)
}
```

**Output**:
```
Error: division by zero
```

**Explanation**:
- The `divide` function returns an error if the divisor is zero.
- The caller explicitly checks for the error and handles it.

---

### Example 2: Using `fmt.Errorf` for Contextual Errors
```go
package main

import (
	"fmt"
)

func readFile(fileName string) error {
	return fmt.Errorf("failed to read file %s: %w", fileName, fmt.Errorf("file not found"))
}

func main() {
	err := readFile("data.txt")
	if err != nil {
		fmt.Println("Error:", err)
	}
}
```

**Output**:
```
Error: failed to read file data.txt: file not found
```

**Explanation**:
- `fmt.Errorf` adds context to the error message, helping to identify the source of the problem.

---

### Example 3: Custom Error Types
```go
package main

import (
	"fmt"
)

type DivideError struct {
	Dividend int
	Divisor  int
}

func (e *DivideError) Error() string {
	return fmt.Sprintf("cannot divide %d by %d", e.Dividend, e.Divisor)
}

func divide(a, b int) (int, error) {
	if b == 0 {
		return 0, &DivideError{Dividend: a, Divisor: b}
	}
	return a / b, nil
}

func main() {
	_, err := divide(10, 0)
	if err != nil {
		fmt.Println("Error:", err)
	}
}
```

**Output**:
```
Error: cannot divide 10 by 0
```

**Explanation**:
- A custom error type (`DivideError`) provides detailed information about the error.

---

### Example 4: Wrapping and Unwrapping Errors
```go
package main

import (
	"errors"
	"fmt"
)

func readConfig() error {
	return errors.New("invalid configuration")
}

func initialize() error {
	err := readConfig()
	if err != nil {
		return fmt.Errorf("initialization failed: %w", err)
	}
	return nil
}

func main() {
	err := initialize()
	if err != nil {
		fmt.Println("Error:", err)

		// Unwrap the error
		unwrapped := errors.Unwrap(err)
		fmt.Println("Underlying Error:", unwrapped)
	}
}
```

**Output**:
```
Error: initialization failed: invalid configuration
Underlying Error: invalid configuration
```

**Explanation**:
- Errors are wrapped using `%w` in `fmt.Errorf`.
- `errors.Unwrap` retrieves the underlying error.

---

### Example 5: Using `errors.Is` and `errors.As`
```go
package main

import (
	"errors"
	"fmt"
)

// Define custom error types
var ErrNotFound = errors.New("resource not found")

type ValidationError struct {
	Field string
	Msg   string
}

func (v *ValidationError) Error() string {
	return fmt.Sprintf("validation error: field '%s' - %s", v.Field, v.Msg)
}

// Simulate a function that returns wrapped errors
func getResource(id int) error {
	if id == 0 {
		return fmt.Errorf("getResource failed: %w", ErrNotFound)
	}
	if id < 0 {
		return &ValidationError{Field: "ID", Msg: "must be a positive number"}
	}
	return nil
}

func main() {
	// Test error handling
	ids := []int{0, -1, 42}
	for _, id := range ids {
		err := getResource(id)
		if err != nil {
			// Check if the error is ErrNotFound using errors.Is
			if errors.Is(err, ErrNotFound) {
				fmt.Printf("ID %d: Error: Resource not found\n", id)
				continue
			}

			// Check if the error is of type ValidationError using errors.As
			var validationErr *ValidationError
			if errors.As(err, &validationErr) {
				fmt.Printf("ID %d: Validation Error: %s\n", id, validationErr)
				continue
			}

			// Generic error handling
			fmt.Printf("ID %d: Unexpected error: %v\n", id, err)
		} else {
			fmt.Printf("ID %d: Resource retrieved successfully\n", id)
		}
	}
}
```

**Output**:
```
ID 0: Error: Resource not found
ID -1: Validation Error: validation error: field 'ID' - must be a positive number
ID 42: Resource retrieved successfully
```

**Explanation**:
- `errors.Is` checks if an error matches a specific error.
- `errors.As` checks if an error is of a specific type.

---

### Example 6: Error Handling in Go Routines
```go
package main

import (
	"errors"
	"fmt"
)

func doTask(results chan error) {
	results <- errors.New("task failed")
}

func main() {
	results := make(chan error, 1)
	go doTask(results)

	err := <-results
	if err != nil {
		fmt.Println("Error:", err)
	}
}
```

**Output**:
```
Error: task failed
```

**Explanation**:
- Errors are sent through a channel to handle errors in goroutines.

---

## Best Practices for Error Handling in Go

1. **Check Errors Explicitly**:
    - Always check the returned error to handle it appropriately.

2. **Add Context to Errors**:
    - Use `fmt.Errorf` or custom error types to add meaningful context to errors.

3. **Avoid Panic for Regular Errors**:
    - Use `panic` only for truly exceptional conditions (e.g., programming errors).

4. **Use Sentinel Errors**:
    - Define reusable `var` errors for common conditions.

5. **Return `nil` for Success**:
    - Return `nil` for the error when there’s no error condition.

6. **Handle Errors Gracefully**:
    - Provide helpful error messages to users or log errors appropriately.

---

## Common Pitfalls

1. **Ignoring Errors**:
    - Avoid ignoring errors by not checking the returned error value.

   ```go
   result, _ := someFunction() // Avoid this
   ```

2. **Overusing `panic`**:
    - `panic` should not be used for normal error handling; it’s reserved for critical failures.

3. **Excessive Wrapping**:
    - Avoid wrapping errors excessively, which can make debugging harder.

---

## Conclusion

Go’s explicit and straightforward error handling model encourages developers to handle errors properly and consistently. With its focus on simplicity, flexibility, and tools like error wrapping, `errors.Is`, and `errors.As`, Go provides a robust framework for managing errors in real-world applications. By following best practices and understanding Go’s error-handling philosophy, developers can write resilient and maintainable software.