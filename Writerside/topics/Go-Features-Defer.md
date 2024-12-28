# Defer

The `defer` statement in Go is used to schedule a function call to be executed at the end of the containing function's execution. Deferred function calls are executed in **last in, first out (LIFO)** order, making it particularly useful for tasks like cleanup, resource management, and debugging.

---

## **How `defer` Works**

1. **Syntax**:
   ```go
   defer functionCall()
   ```
   The `functionCall` is scheduled to execute just before the surrounding function returns.

2. **LIFO Order**:
   Multiple deferred calls are executed in the reverse order of their declaration.

---

## **Basic Example**

```go
package main

import "fmt"

func main() {
	defer fmt.Println("This runs last")
	fmt.Println("This runs first")
}
```

**Output:**
```
This runs first
This runs last
```

---

## **Deferred Function Calls Are Executed LIFO**

```go
package main

import "fmt"

func main() {
	defer fmt.Println("First deferred call")
	defer fmt.Println("Second deferred call")
	defer fmt.Println("Third deferred call")
	fmt.Println("Main function executed")
}
```

**Output:**
```
Main function executed
Third deferred call
Second deferred call
First deferred call
```

Explanation: Deferred calls are executed in reverse order, starting with the last deferred call.

---

## **Defer with Function Arguments**

Arguments to a deferred function are evaluated immediately, but the function execution is delayed.

### Example 1:

```go
package main

import "fmt"

func main() {
	x := 5
	defer fmt.Println("Deferred value of x:", x)
	x = 10
	fmt.Println("Current value of x:", x)
}
```

**Output:**
```
Current value of x: 10
Deferred value of x: 5
```

Explanation: When `defer` is declared, the value of `x` (5) is captured and used when the deferred function executes.

---

## **Practical Use Cases**

### 1. **Resource Cleanup**

Defer is commonly used to close resources like files, network connections, or database transactions.

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	file, err := os.Create("example.txt")
	if err != nil {
		fmt.Println("Error creating file:", err)
		return
	}
	defer file.Close() // Ensure the file is closed when the function exits

	file.WriteString("Hello, Go!")
	fmt.Println("File written successfully")
}
```

**Explanation**: `defer file.Close()` ensures that the file is closed regardless of how the function exits, whether normally or due to an error.

---

### 2. **Unlocking a Mutex**

```go
package main

import (
	"fmt"
	"sync"
)

func main() {
	var mu sync.Mutex

	mu.Lock()
	defer mu.Unlock() // Ensure the mutex is unlocked

	fmt.Println("Critical section")
}
```

**Explanation**: Using `defer` ensures that the mutex is always unlocked, even if the function exits prematurely.

---

### 3. **Releasing Memory or Cleanup**

```go
package main

import "fmt"

func main() {
	data := []int{1, 2, 3, 4}
	defer fmt.Println("Cleaning up memory:", data)

	fmt.Println("Processing data:", data)
}
```

**Output:**
```
Processing data: [1 2 3 4]
Cleaning up memory: [1 2 3 4]
```

---

## **Defer in Error Handling**

Defer is often used in conjunction with `recover` to handle panics gracefully.

### Example: Recovering from Panic
```go
package main

import "fmt"

func main() {
	defer func() {
		if r := recover(); r != nil {
			fmt.Println("Recovered from panic:", r)
		}
	}()

	fmt.Println("About to cause a panic")
	panic("Something went wrong")
}
```

**Output:**
```
About to cause a panic
Recovered from panic: Something went wrong
```

**Explanation**: The deferred function captures the panic using `recover` and prevents the program from crashing.

---

## **Defer with Anonymous Functions**

You can use `defer` with inline anonymous functions.

```go
package main

import "fmt"

func main() {
	defer func() {
		fmt.Println("Deferred anonymous function executed")
	}()
	fmt.Println("Main function executed")
}
```

**Output:**
```
Main function executed
Deferred anonymous function executed
```

---

## **Using Defer in Loops**

Be cautious when using `defer` inside loops, as all deferred calls are executed at the end of the function.

### Example 2:

```go
package main

import "fmt"

func main() {
	for i := 0; i < 3; i++ {
		defer fmt.Println("Deferred:", i)
	}
}
```

**Output:**
```
Deferred: 2
Deferred: 1
Deferred: 0
```

**Explanation**: The `defer` statements are executed in reverse order, and the value of `i` at each iteration is captured immediately.

---

## **Defer with Multiple Return Values**

Deferred functions can interact with named return values in a function.

### Example 3:

```go
package main

import "fmt"

func example() (result int) {
	defer func() {
		result += 5
	}()
	return 10
}

func main() {
	fmt.Println("Result:", example())
}
```

**Output:**
```
Result: 15
```

**Explanation**: The deferred function modifies the named return value `result` after the `return` statement but before the function exits.

---

## **Best Practices with Defer**

1. **Use for Cleanup Tasks**: Use `defer` for closing files, unlocking resources, or releasing memory.
2. **Avoid in Tight Loops**: Using `defer` inside loops can lead to unexpected memory consumption since all deferred calls are queued.
3. **Understand Argument Evaluation**: Remember that arguments to deferred functions are evaluated immediately.
4. **Limit Complexity**: Avoid overly complex logic in deferred functions to maintain readability.

---

## **Summary**

The `defer` statement is a versatile tool in Go for managing resource cleanup and ensuring tasks are completed before a function exits. Its LIFO execution order, interaction with return values, and integration with `recover` make it an essential feature for writing robust and maintainable Go code.