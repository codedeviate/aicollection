# Context Package

The `context` package in Go is used to carry deadlines, cancellation signals, and other request-scoped values across API boundaries and between goroutines. It provides a way to control the lifetime of processes, manage resource cleanup, and prevent goroutine leaks in concurrent applications. Below is an in-depth explanation of how the `context` package works, along with several illustrative examples.

---

## Key Concepts

1. **`Context` Interface**
   ```go
   type Context interface {
       Deadline() (deadline time.Time, ok bool)
       Done() <-chan struct{}
       Err() error
       Value(key interface{}) interface{}
   }
   ```
    - **`Deadline()`**: Returns the time when work should be canceled, and a boolean indicating if a deadline is set.
    - **`Done()`**: Returns a channel that is closed when work should be canceled.
    - **`Err()`**: Returns a non-nil error if the context is canceled or has expired.
    - **`Value()`**: Retrieves any stored data associated with the context.

2. **Context Types and Functions**
    - **`context.Background()`**: Returns an empty context. It’s the root context usually used at the start of main functions or servers.
    - **`context.TODO()`**: Returns an empty context when you are not sure which context to use or planning to add it later.
    - **`context.WithCancel(parent)`**: Returns a copy of the parent context with a new `Done()` channel that can be closed by calling the cancel function.
    - **`context.WithDeadline(parent, deadlineTime)`**: Similar to `WithCancel`, but automatically closes the `Done()` channel at a specified time.
    - **`context.WithTimeout(parent, duration)`**: A convenience wrapper over `WithDeadline` that ends the context after a duration.
    - **`context.WithValue(parent, key, val)`**: Returns a copy of the parent context with an associated key-value pair. Good for passing request-scoped data down a call chain.

---

## 1. Using `context.WithCancel`

`WithCancel` creates a context that can be canceled manually. When you call the cancel function, the `Done` channel in the context is closed, signaling any goroutines using that context to stop work if they wish to respect cancellation.

### Example: Manual Cancellation

```go
package main

import (
    "context"
    "fmt"
    "time"
)

func main() {
    // Create a base context
    ctx := context.Background()

    // Create a cancellable context
    ctx, cancel := context.WithCancel(ctx)

    // Start a goroutine that does some work
    go func() {
        // Use a loop to mimic some ongoing work
        for {
            select {
            case <-ctx.Done():
                // Context was canceled
                fmt.Println("Worker: context canceled, stopping...")
                return
            default:
                fmt.Println("Worker: working...")
                time.Sleep(500 * time.Millisecond)
            }
        }
    }()

    // Let the worker run for 2 seconds
    time.Sleep(2 * time.Second)

    // Cancel the context
    fmt.Println("Main: canceling context...")
    cancel()

    // Wait a bit to see the goroutine exit
    time.Sleep(1 * time.Second)
    fmt.Println("Main: done")
}
```

#### Explanation 1
- We create a root context with `context.Background()`.
- `context.WithCancel(ctx)` returns a derived context and a `cancel` function.
- The goroutine continuously checks for cancellation via `select { case <-ctx.Done(): ... }`.
- When `cancel()` is called, `ctx.Done()` is closed, signaling the goroutine to stop.

**Sample Output** (truncated):
```
Worker: working...
Worker: working...
Worker: working...
Main: canceling context...
Worker: context canceled, stopping...
Main: done
```

---

## 2. Using `context.WithTimeout` and `context.WithDeadline`

`WithTimeout` automatically cancels the context after a specified duration, whereas `WithDeadline` cancels the context at a specific time.

### Example: Automatic Cancellation with Timeout

```go
package main

import (
    "context"
    "fmt"
    "time"
)

func main() {
    // Create a context with a 2-second timeout
    ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
    defer cancel() // Always call cancel to free resources

    go func() {
        <-ctx.Done()
        fmt.Println("Goroutine: context done:", ctx.Err())
    }()

    // Simulate some work that takes 3 seconds
    select {
    case <-time.After(3 * time.Second):
        fmt.Println("Main: finished work without cancellation")
    case <-ctx.Done():
        fmt.Println("Main: context canceled:", ctx.Err())
    }
}
```

#### Explanation 2
- `context.WithTimeout` sets up a 2-second limit for the derived context.
- If the work (`time.After(3 * time.Second)`) takes longer than 2 seconds, the context will expire, and `ctx.Err()` will be `context.DeadlineExceeded`.
- If the work finishes before 2 seconds, the context wouldn’t be canceled early, but you still call `cancel()` in a `defer` to release any resources.

**Sample Output** (if it times out):
```
Main: context canceled: context deadline exceeded
Goroutine: context done: context deadline exceeded
```

---

## 3. Passing Values in Context

Although the `context` package allows adding and retrieving values with `WithValue`, it is intended for request-scoped data (like user IDs, request IDs, or authentication tokens) and not for passing large data structures.

### Example: Adding and Retrieving Values

```go
package main

import (
    "context"
    "fmt"
)

type key string

const userIDKey key = "userID"

func main() {
    ctx := context.Background()

    // Store a user ID in the context
    ctx = context.WithValue(ctx, userIDKey, "12345")

    processRequest(ctx)
}

func processRequest(ctx context.Context) {
    // Retrieve the user ID from context
    userID, ok := ctx.Value(userIDKey).(string)
    if !ok {
        fmt.Println("No user ID found in context")
        return
    }
    fmt.Println("processRequest: user ID is", userID)
}
```

#### Explanation 3
- We define a custom type `key string` to avoid collisions in case other packages also store strings in context.
- `WithValue(ctx, userIDKey, "12345")` returns a new context with user ID = `"12345"`.
- We retrieve it via `ctx.Value(userIDKey)`, and if it matches type `string`, we use it.

**Sample Output**:
```
processRequest: user ID is 12345
```

---

## 4. Cancelling Multiple Goroutines

Multiple goroutines can share the same context to signal a coordinated cancellation. When `cancel()` is called or a timeout is reached, all goroutines that derive from that context see `ctx.Done()` close.

### Example: Coordinating Cancellation

```go
package main

import (
    "context"
    "fmt"
    "time"
)

func main() {
    ctx, cancel := context.WithTimeout(context.Background(), 3*time.Second)
    defer cancel()

    for i := 0; i < 3; i++ {
        go worker(ctx, i)
    }

    // Wait for a while
    time.Sleep(5 * time.Second)
    fmt.Println("Main: all done")
}

func worker(ctx context.Context, id int) {
    for {
        select {
        case <-ctx.Done():
            fmt.Printf("Worker %d: done, reason: %v\n", id, ctx.Err())
            return
        default:
            fmt.Printf("Worker %d: working...\n", id)
            time.Sleep(1 * time.Second)
        }
    }
}
```

#### Explanation 4
- We create a single context with a 3-second timeout and spawn three goroutines.
- Each goroutine checks for `ctx.Done()`. After 3 seconds, `ctx.Err()` becomes `context.DeadlineExceeded`, causing all workers to exit.

**Sample Output** (truncated):
```
Worker 0: working...
Worker 1: working...
Worker 2: working...
Worker 0: working...
Worker 1: working...
Worker 2: working...
Worker 0: done, reason: context deadline exceeded
Worker 1: done, reason: context deadline exceeded
Worker 2: done, reason: context deadline exceeded
Main: all done
```

---

## 5. Nested Contexts

You can derive multiple child contexts from a parent, each potentially with its own deadline or cancellation rule. Canceling or timing out the parent automatically cancels all children.

### Example: Nested Contexts

```go
package main

import (
    "context"
    "fmt"
    "time"
)

func main() {
    rootCtx := context.Background()
    
    // Create a parent context with a 3-second timeout
    parentCtx, parentCancel := context.WithTimeout(rootCtx, 3*time.Second)
    defer parentCancel()

    // Create a child context with a 2-second timeout
    childCtx, childCancel := context.WithTimeout(parentCtx, 2*time.Second)
    defer childCancel()

    go func() {
        // Child will see Done if it hits 2s or if parent hits 3s first
        <-childCtx.Done()
        fmt.Println("Child context done:", childCtx.Err())
    }()

    go func() {
        <-parentCtx.Done()
        fmt.Println("Parent context done:", parentCtx.Err())
    }()

    time.Sleep(4 * time.Second)
    fmt.Println("Main: finished")
}
```

#### Explanation 5
- The child context will finish in 2 seconds, triggering `childCtx.Err() = context.DeadlineExceeded`.
- The parent context will finish in 3 seconds.
- If the parent finishes earlier, it cancels the child as well.

**Sample Output** (order may vary):
```
Child context done: context deadline exceeded
Parent context done: context deadline exceeded
Main: finished
```

---

## 6. Best Practices

1. **Pass `context.Context` as the first parameter**
    - Conventional signature: `func DoSomething(ctx context.Context, arg1 Type1, ...)`.

2. **Do Not Store Contexts in Struct Fields**
    - Contexts are request-scoped or operation-scoped; storing them in a struct can lead to confusion about their lifetime.

3. **Use `context.TODO()` Sparingly**
    - `context.TODO()` is a placeholder. Replace it with a proper context once you know the lifetime or cancellation needs.

4. **Avoid Putting Large Objects in Context**
    - Use `context.WithValue` for request-scoped data like request IDs, not for large data structures.

5. **Always Call `cancel()`**
    - If you create a context with `WithCancel`, `WithTimeout`, or `WithDeadline`, call the cancel function to release resources (especially in library code).

6. **Check `ctx.Err()`**
    - If you’re performing expensive operations or waiting for I/O, periodically check `ctx.Err()` or `ctx.Done()` to handle cancellations promptly.

---

## Conclusion

The `context` package is a vital tool in Go for managing cancellations, timeouts, and request-scoped data in concurrent applications. By following Go’s conventions—such as making `context.Context` the first parameter in functions, respecting cancellation signals, and passing only small amounts of data—you can write robust, leak-free, and well-structured code. Whether you’re building microservices, CLI tools, or background workers, using context effectively ensures that your goroutines do not outlive their purpose and that your code handles timeouts and cancellations gracefully.