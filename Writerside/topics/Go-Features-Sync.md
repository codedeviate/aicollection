# Sync

The `sync` package in Go provides a variety of synchronization primitives to handle concurrency safely and efficiently. It includes mechanisms like `Mutex`, `RWMutex`, `WaitGroup`, `Once`, and `Cond`, which are essential for coordinating goroutines, protecting shared resources, and ensuring proper execution order.

---

## **Key Features of the `sync` Package**

1. **Mutex and RWMutex**:
    - Used for mutual exclusion to protect shared resources.
    - `Mutex` is for exclusive access, while `RWMutex` allows multiple readers or one writer.

2. **WaitGroup**:
    - Used to wait for a collection of goroutines to finish.

3. **Once**:
    - Ensures a block of code is executed only once, even in concurrent scenarios.

4. **Cond**:
    - Implements condition variables for signaling between goroutines.

---

## **1. Mutex**

A `Mutex` is used to protect shared resources by allowing only one goroutine to access a critical section at a time.

### Example: Using `sync.Mutex`

```go
package main

import (
	"fmt"
	"sync"
)

type Counter struct {
	mu    sync.Mutex
	value int
}

func (c *Counter) Increment() {
	c.mu.Lock()
	defer c.mu.Unlock() // Ensure the mutex is unlocked
	c.value++
}

func (c *Counter) Value() int {
	c.mu.Lock()
	defer c.mu.Unlock()
	return c.value
}

func main() {
	counter := Counter{}
	wg := sync.WaitGroup{}

	for i := 0; i < 10; i++ {
		wg.Add(1)
		go func() {
			defer wg.Done()
			counter.Increment()
		}()
	}

	wg.Wait()
	fmt.Println("Final Counter Value:", counter.Value())
}
```

**Output:**
```
Final Counter Value: 10
```

**Explanation**: The `sync.Mutex` ensures that only one goroutine increments the counter at a time, avoiding race conditions.

---

## **2. RWMutex**

An `RWMutex` (Read-Write Mutex) allows multiple readers but only one writer at a time.

### Example: Using `sync.RWMutex`

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

type SafeMap struct {
	mu   sync.RWMutex
	data map[string]string
}

func (sm *SafeMap) Write(key, value string) {
	sm.mu.Lock()
	defer sm.mu.Unlock()
	sm.data[key] = value
}

func (sm *SafeMap) Read(key string) string {
	sm.mu.RLock()
	defer sm.mu.RUnlock()
	return sm.data[key]
}

func main() {
	sm := SafeMap{data: make(map[string]string)}
	wg := sync.WaitGroup{}

	// Writing to the map
	wg.Add(1)
	go func() {
		defer wg.Done()
		sm.Write("name", "GoLang")
	}()

	// Reading from the map
	wg.Add(1)
	go func() {
		defer wg.Done()
		time.Sleep(1 * time.Second)
		fmt.Println("Name:", sm.Read("name"))
	}()

	wg.Wait()
}
```

**Output:**
```
Name: GoLang
```

**Explanation**: The `sync.RWMutex` allows concurrent reads but ensures exclusive access for writes.

---

## **3. WaitGroup**

A `WaitGroup` is used to wait for multiple goroutines to finish execution.

### Example: Using `sync.WaitGroup`

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

func worker(id int, wg *sync.WaitGroup) {
	defer wg.Done() // Mark this goroutine as done
	fmt.Printf("Worker %d starting\n", id)
	time.Sleep(time.Second)
	fmt.Printf("Worker %d done\n", id)
}

func main() {
	var wg sync.WaitGroup

	for i := 1; i <= 3; i++ {
		wg.Add(1) // Increment the counter
		go worker(i, &wg)
	}

	wg.Wait() // Wait for all goroutines to finish
	fmt.Println("All workers completed")
}
```

**Output:**
```
Worker 1 starting
Worker 2 starting
Worker 3 starting
Worker 1 done
Worker 2 done
Worker 3 done
All workers completed
```

**Explanation**: The `sync.WaitGroup` ensures the main goroutine waits for all worker goroutines to finish before proceeding.

---

## **4. Once**

A `Once` ensures that a block of code executes only once, no matter how many times it is called or in how many goroutines.

### Example: Using `sync.Once`

```go
package main

import (
	"fmt"
	"sync"
)

func main() {
	var once sync.Once
	wg := sync.WaitGroup{}

	initialize := func() {
		fmt.Println("Initialization executed")
	}

	for i := 0; i < 5; i++ {
		wg.Add(1)
		go func() {
			defer wg.Done()
			once.Do(initialize)
		}()
	}

	wg.Wait()
}
```

**Output:**
```
Initialization executed
```

**Explanation**: The `sync.Once` ensures that `initialize` is called only once, even though multiple goroutines try to execute it.

---

## **5. Cond**

A `Cond` provides signaling for goroutines to wait for or broadcast events.

### Example: Using `sync.Cond`

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

func main() {
	var mu sync.Mutex
	cond := sync.NewCond(&mu)
	queue := []int{}

	removeFromQueue := func(delay time.Duration) {
		time.Sleep(delay)
		mu.Lock()
		queue = queue[1:]
		fmt.Println("Removed from queue")
		cond.Signal() // Notify waiting goroutine
		mu.Unlock()
	}

	for i := 0; i < 3; i++ {
		mu.Lock()
		for len(queue) == 2 {
			cond.Wait() // Wait until there's space in the queue
		}
		queue = append(queue, i)
		fmt.Println("Added to queue:", i)
		go removeFromQueue(1 * time.Second)
		mu.Unlock()
	}
	time.Sleep(2 * time.Second)
}
```

**Output:**
```
Added to queue: 0
Added to queue: 1
Removed from queue
Added to queue: 2
Removed from queue
Removed from queue
```

**Explanation**: The `sync.Cond` allows one or more goroutines to wait for a condition and proceed when the condition is signaled.

---

## **Best Practices with `sync`**

1. **Avoid Overuse**: Use `sync` primitives judiciously. Go's channels and other high-level constructs often provide simpler solutions.
2. **Avoid Deadlocks**: Be cautious with `Lock` and `Unlock` to prevent situations where two or more goroutines wait indefinitely.
3. **Use `RWMutex` for Performance**: Use `sync.RWMutex` when multiple readers are expected to reduce contention.
4. **Always Call `Unlock` in Defer**: To ensure locks are released even if a function exits unexpectedly.
   ```go
   mu.Lock()
   defer mu.Unlock()
   ```
5. **Initialize Shared Structures**: Always initialize shared structures like maps or slices before accessing them in multiple goroutines.

---

## **Summary**

The `sync` package provides low-level tools to coordinate goroutines and manage shared resources. While these primitives are powerful, they should be used thoughtfully to avoid complexity and ensure code correctness. With the right approach, `sync` enables safe and efficient concurrency in Go applications.