# Goroutines

Goroutines are lightweight threads of execution in the Go programming language, enabling concurrent programming by running multiple tasks simultaneously. They are a key feature in Go, designed to simplify concurrent programming and improve efficiency. Here's an in-depth look, including examples:

---

## What are Goroutines?
A goroutine is a function or method that executes concurrently with other goroutines. They are managed by the Go runtime rather than the operating system, making them lightweight compared to traditional threads. Goroutines are started with the `go` keyword.

**Key Features:**
- **Lightweight**: Thousands of goroutines can run simultaneously in the same application.
- **Dynamic Scheduling**: The Go runtime handles scheduling, allowing efficient use of resources.
- **Communication**: Goroutines communicate and synchronize using channels.

---

## How to Create a Goroutine

To start a goroutine, use the `go` keyword before a function call.

```go
package main

import (
	"fmt"
	"time"
)

func sayHello() {
	for i := 0; i < 5; i++ {
		fmt.Println("Hello")
		time.Sleep(100 * time.Millisecond)
	}
}

func main() {
	go sayHello() // Start the goroutine
	for i := 0; i < 5; i++ {
		fmt.Println("World")
		time.Sleep(200 * time.Millisecond)
	}
}
```

**Output:**
The output alternates between "Hello" and "World" because `sayHello` and the main function run concurrently.

Note that the main function will not wait for the goroutine to finish.
If you want to wait for a goroutine to complete, you can use synchronization mechanisms like channels or `sync.WaitGroup`.

If the main function exits, all goroutines are terminated.
That's the reason why the sleep is longer in the main function than in the goroutine.

---

## Anonymous Goroutines

You can start a goroutine with an anonymous function:

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	go func() {
		for i := 0; i < 5; i++ {
			fmt.Println("Inside goroutine")
			time.Sleep(100 * time.Millisecond)
		}
	}()
	
	fmt.Println("Main function")
	time.Sleep(600 * time.Millisecond)
}
```

**Output:**
The "Inside goroutine" messages appear while the main function is running.

---

## Using Channels with Goroutines

Channels are used to communicate between goroutines safely.

### Example 1: Sending and Receiving Data
```go
package main

import "fmt"

func sendMessage(ch chan string) {
	ch <- "Hello from goroutine"
}

func main() {
	ch := make(chan string)

	go sendMessage(ch)

	msg := <-ch // Receive message
	fmt.Println(msg)
}
```

**Output:**
```
Hello from goroutine
```

### Example 2: Buffered Channels
```go
package main

import "fmt"

func main() {
	ch := make(chan int, 3) // Create a buffered channel

	ch <- 1
	ch <- 2
	ch <- 3

	fmt.Println(<-ch) // Output: 1
	fmt.Println(<-ch) // Output: 2
	fmt.Println(<-ch) // Output: 3
}
```

---

## Goroutines and Synchronization

Without proper synchronization, goroutines can cause race conditions. Use the `sync.WaitGroup` to wait for multiple goroutines to finish.

```go
package main

import (
	"fmt"
	"sync"
)

func printNumber(wg *sync.WaitGroup, num int) {
	defer wg.Done() // Mark as done
	fmt.Println(num)
}

func main() {
	var wg sync.WaitGroup

	for i := 1; i <= 5; i++ {
		wg.Add(1) // Increment counter
		go printNumber(&wg, i)
	}

	wg.Wait() // Wait for all goroutines to finish
	fmt.Println("All goroutines completed")
}
```

---

## Common Use Cases

1. **Web Servers**
   Goroutines handle multiple client requests concurrently in web servers.

   ```go
   package main

   import (
	   "fmt"
	   "net/http"
   )

   func handler(w http.ResponseWriter, r *http.Request) {
	   fmt.Fprintf(w, "Hello, World!")
   }

   func main() {
	   http.HandleFunc("/", handler)
	   http.ListenAndServe(":8080", nil)
   }
   ```

   Each HTTP request is handled in its own goroutine internally.

2. **Parallel Processing**
   Splitting tasks across multiple goroutines for parallel computation.

   ```go
   package main

   import (
	   "fmt"
	   "sync"
   )

   func compute(wg *sync.WaitGroup, id int) {
	   defer wg.Done()
	   fmt.Printf("Task %d started\n", id)
   }

   func main() {
	   var wg sync.WaitGroup

	   for i := 1; i <= 3; i++ {
		   wg.Add(1)
		   go compute(&wg, i)
	   }

	   wg.Wait()
	   fmt.Println("All tasks completed")
   }
   ```

---

## Key Considerations
1. **Avoid Goroutine Leaks**: Ensure goroutines terminate or have a proper way to exit to avoid memory leaks.
2. **Shared State**: Use channels or sync primitives (e.g., `sync.Mutex`) to manage shared data.
3. **Panic Recovery**: Use `defer` and `recover` to handle panics within goroutines.

By using goroutines effectively, you can build highly concurrent and efficient applications in Go.