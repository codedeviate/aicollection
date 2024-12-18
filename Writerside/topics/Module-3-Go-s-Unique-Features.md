# Module 3: Go’s Unique Features

## Detailed Topics:

### Pointers and Memory
Go’s pointers allow you to work with memory addresses directly, but they differ significantly from C++ pointers. In Go:
- There is no pointer arithmetic, making them safer to use.
- Variables and pointers are garbage collected, reducing the risk of memory leaks.

#### Example 1:
```go
package main
import "fmt"

func main() {
    x := 42
    p := &x // Pointer to x
    fmt.Println(*p) // Dereference pointer to get value

    *p = 21 // Modify value through the pointer
    fmt.Println(x) // Prints 21
}
```

### Concurrency
Concurrency is a core feature of Go, achieved through goroutines and channels. Goroutines are lightweight threads, while channels facilitate safe communication between them. The `select` statement allows you to wait on multiple channel operations.

#### Example 2:
```go
package main
import (
    "fmt"
    "time"
)

func worker(id int, ch chan string) {
    for msg := range ch {
        fmt.Printf("Worker %d received: %s\n", id, msg)
    }
}

func main() {
    ch := make(chan string)
    go worker(1, ch)
    go worker(2, ch)

    for i := 0; i < 5; i++ {
        ch <- fmt.Sprintf("Task %d", i)
    }
    close(ch)
    time.Sleep(time.Second) // Ensure workers finish
}
```

### Error Handling
Go emphasizes explicit error handling using error values. Functions often return errors as their last return value, enabling straightforward checking.

#### Example 3:
```go
package main
import (
    "fmt"
    "os"
)

func readFile(filename string) error {
    file, err := os.Open(filename)
    if err != nil {
        return fmt.Errorf("failed to open file: %w", err)
    }
    defer file.Close()

    buf := make([]byte, 1024)
    _, err = file.Read(buf)
    if err != nil {
        return fmt.Errorf("failed to read file: %w", err)
    }
    fmt.Println(string(buf))
    return nil
}

func main() {
    err := readFile("example.txt")
    if err != nil {
        fmt.Println("Error:", err)
    }
}
```

## Detailed Hands-On:

### 1. Create a Multi-Threaded Counter Using Goroutines
**Goal**: Use goroutines and channels to safely increment a shared counter.

#### Example 4:
```go
package main
import (
    "fmt"
    "sync"
)

func main() {
    counter := 0
    var mu sync.Mutex
    var wg sync.WaitGroup

    for i := 0; i < 10; i++ {
        wg.Add(1)
        go func() {
            mu.Lock()
            counter++
            mu.Unlock()
            wg.Done()
        }()
    }

    wg.Wait()
    fmt.Println("Final Counter:", counter)
}
```

### 2. Synchronize with Buffered and Unbuffered Channels
**Goal**: Use buffered and unbuffered channels to coordinate goroutines.

#### Example 5:
```go
package main
import "fmt"

func producer(ch chan int) {
    for i := 0; i < 5; i++ {
        ch <- i
        fmt.Println("Produced:", i)
    }
    close(ch)
}

func consumer(ch chan int) {
    for item := range ch {
        fmt.Println("Consumed:", item)
    }
}

func main() {
    ch := make(chan int, 2) // Buffered channel
    go producer(ch)
    consumer(ch)
}
```

### 3. Write Error-Handling Functions for File Operations
**Goal**: Implement idiomatic error handling in file operations.

#### Example 6:
```go
package main
import (
    "fmt"
    "os"
)

func writeFile(filename string, content string) error {
    file, err := os.Create(filename)
    if err != nil {
        return fmt.Errorf("could not create file: %w", err)
    }
    defer file.Close()

    _, err = file.WriteString(content)
    if err != nil {
        return fmt.Errorf("could not write to file: %w", err)
    }
    return nil
}

func main() {
    err := writeFile("output.txt", "Hello, Go!")
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("File written successfully!")
    }
}
```

