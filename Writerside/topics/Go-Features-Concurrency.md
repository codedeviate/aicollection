# Concurrency


## Concurrency in Go

Go’s concurrency model is built around **goroutines** and **channels**. A goroutine is a lightweight thread of execution managed by the Go runtime, rather than the operating system. Because goroutines are extremely cheap, Go makes it practical to design programs that spin up thousands or even millions of goroutines when needed.

### Goroutines and Processors

By default, Go schedules all active goroutines across as many processors (CPUs) as it sees available. However, you can customize the number of CPUs the Go runtime is allowed to use with **`runtime.GOMAXPROCS`**. This function sets the maximum number of OS threads that can execute user-level Go code simultaneously, effectively controlling parallelism.

---

## Basic Goroutine Example

```go
package main

import (
    "fmt"
    "time"
)

func sayHello() {
    fmt.Println("Hello from goroutine")
}

func main() {
    go sayHello() // start a new goroutine
    fmt.Println("Hello from main")

    // Wait for goroutine to finish (for demo only; use sync in real code)
    time.Sleep(time.Second)
}
```

**Explanation**:
- `go sayHello()` spawns a new goroutine running `sayHello()` concurrently with `main`.
- `time.Sleep(time.Second)` is a rudimentary wait to let the goroutine complete before the program exits.

---

## Using Multiple CPUs with Goroutines

In Go, you can utilize goroutines to run code concurrently on multiple processors. The `runtime` package provides functionality to control how many processors (or CPUs) Go uses.

### Steps:
1. **Use Goroutines**: To run tasks concurrently.
2. **Use `runtime.GOMAXPROCS`**: To set the maximum number of CPUs that Go should utilize.
3. **Use `sync.WaitGroup` or Channels**: To synchronize or wait for all goroutines to finish.

### Example Code:

```go
package main

import (
    "fmt"
    "runtime"
    "sync"
)

func task(id int) {
    fmt.Printf("Task %d is running\n", id)
}

func main() {
    // Determine and set the maximum number of processors (CPUs) that Go should use
    numCPUs := runtime.NumCPU()
    runtime.GOMAXPROCS(numCPUs)

    var wg sync.WaitGroup

    // Launch multiple goroutines
    for i := 1; i <= 10; i++ {
        wg.Add(1) // Increment the WaitGroup counter
        go func(id int) {
            defer wg.Done() // Decrement when the goroutine completes
            task(id)
        }(i)
    }

    // Wait for all goroutines to complete
    wg.Wait()

    fmt.Println("All tasks completed.")
}
```

#### Explanation:
- **`runtime.NumCPU()`** finds the number of logical CPUs available on the system.
- **`runtime.GOMAXPROCS(numCPUs)`** tells Go to use all those CPUs for parallel execution (you can adjust this to any integer up to `numCPUs`).
- A **`sync.WaitGroup`** is used to wait for all goroutines to finish before the program exits.
- In this example, each goroutine runs the `task(id)` function, simulating concurrent tasks.

**Key Points**:
- **Goroutines** are lightweight, making it practical to launch many of them for concurrent or parallel operations.
- **`runtime.GOMAXPROCS`** lets you tune how many CPU cores the Go scheduler may utilize. By default, Go uses all available cores, but you can limit or expand usage based on your needs.
- **Channels** or **`sync.WaitGroup`** can be used for synchronization. Here, `WaitGroup` is the simpler choice to just block until all goroutines complete.

---

## Channels for Communication

While `sync.WaitGroup` helps wait for goroutines to finish, **channels** provide a way to pass data between goroutines safely and synchronize their execution. For instance:

### Producer-Consumer with Channels

```go
package main

import (
    "fmt"
)

func producer(ch chan<- int) {
    for i := 0; i < 5; i++ {
        ch <- i
    }
    close(ch)
}

func consumer(ch <-chan int, done chan<- bool) {
    for val := range ch {
        fmt.Println("Consumed:", val)
    }
    done <- true
}

func main() {
    ch := make(chan int)
    done := make(chan bool)

    go producer(ch)
    go consumer(ch, done)

    <-done // Wait for consumer to signal it's done
    fmt.Println("All values consumed.")
}
```

**Explanation**:
- `ch` is an unbuffered channel for integers.
- **`producer`** sends values `0..4` into `ch` and then closes it.
- **`consumer`** reads from `ch` until it’s closed, printing the received values.
- The **`done`** channel signals the main goroutine that the consumer is finished, avoiding premature program exit.

---

## Synchronization Primitives

Besides channels, the **`sync`** package provides additional concurrency tools:

- **`sync.Mutex`** and **`sync.RWMutex`**: For protecting shared data with locks.
- **`sync.Cond`**: For advanced conditional synchronization.
- **`sync.Map`**: A concurrent map implementation with optimized operations under certain workloads.

Here’s a quick example with a **`sync.Mutex`**:

```go
package main

import (
    "fmt"
    "sync"
)

type SafeCounter struct {
    mu    sync.Mutex
    value int
}

func (sc *SafeCounter) Increment() {
    sc.mu.Lock()
    defer sc.mu.Unlock()
    sc.value++
}

func (sc *SafeCounter) Value() int {
    sc.mu.Lock()
    defer sc.mu.Unlock()
    return sc.value
}

func main() {
    sc := &SafeCounter{}

    var wg sync.WaitGroup
    for i := 0; i < 100; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            sc.Increment()
        }()
    }
    wg.Wait()

    fmt.Println("Final counter value:", sc.Value())
}
```

**Explanation**:
- The **`SafeCounter`** uses a **`sync.Mutex`** to ensure that increments do not race each other.
- Without the lock, multiple goroutines could increment the value at the same time, leading to race conditions and incorrect counts.

---

## Concurrency vs. Parallelism

- **Concurrency**: Structuring a program as multiple independent tasks that can run out of order or in partial order, without necessarily running in parallel.
- **Parallelism**: Physically executing multiple tasks at the same time on different CPU cores.

Go provides concurrency primitives via goroutines and channels, and you can achieve parallel execution by running goroutines on multiple cores (as showcased by adjusting **`runtime.GOMAXPROCS`**).

---

## Common Pitfalls

1. **Goroutine Leaks**:
    - Always ensure goroutines have a clear exit path or they may leak and remain blocked indefinitely (e.g., stuck on a channel read with no writes).

2. **Data Races**:
    - Occur when two or more goroutines access the same variable simultaneously, and at least one modifies it. Use channels or locks to protect shared data.

3. **Deadlocks**:
    - Two or more goroutines waiting on each other’s locks or channels indefinitely.

4. **Excessive Goroutines**:
    - While goroutines are cheap, creating millions of them without structure can degrade performance or consume memory.

---

## Conclusion

Go’s concurrency model—centered on goroutines and channels—offers a simple yet powerful way to write highly concurrent (and potentially parallel) programs. By using **`runtime.GOMAXPROCS`**, you can fine-tune how many CPU cores the scheduler may employ, allowing tasks to run in parallel for improved performance on multi-core systems. Tools like **`sync.WaitGroup`**, **`sync.Mutex`**, and channels help coordinate goroutines safely. With these constructs, Go encourages writing clear, robust concurrent code that scales effectively across many cores and workloads.

---