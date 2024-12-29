# Standard Library

The **standard library** in Go is a rich set of packages that provide essential functionality for building applications without requiring external dependencies. It includes tools for file manipulation, networking, cryptography, data structures, text processing, and much more.

Below, we'll explore key aspects of the standard library and provide examples to demonstrate its functionality.

---

## 1. Basic Utilities

### fmt Package (Formatted I/O)
The `fmt` package provides functions for formatted output and input.

**Example: Formatted Output**
```go
package main

import "fmt"

func main() {
	name := "Alice"
	age := 30
	fmt.Printf("Name: %s, Age: %d\n", name, age) // Format strings
	fmt.Println("Hello", name)                  // Print with a newline
}
```

**Output:**
```
Name: Alice, Age: 30
Hello Alice
```

---

### time Package (Date and Time)
The `time` package provides functionality for working with dates and times.

**Example: Get Current Time**
```go
package main

import (
	"fmt"
	"time"
)

func main() {
	now := time.Now()
	fmt.Println("Current Time:", now)

	// Formatting time
	fmt.Println("Formatted:", now.Format("2006-01-02 15:04:05"))

	// Adding time
	later := now.Add(2 * time.Hour)
	fmt.Println("Two Hours Later:", later)
}
```

**Output:**
```
Current Time: 2024-12-28 15:00:00.000000
Formatted: 2024-12-28 15:00:00
Two Hours Later: 2024-12-28 17:00:00
```

**Note**: The reference date for formatting in Go is `Mon Jan 2 15:04:05 MST 2006`.

---

## 2. File and Directory Operations

### os and ioutil Packages
The `os` package provides low-level operating system functions, while `io/ioutil` (deprecated in Go 1.16, replaced by `os` and `io`) simplifies file handling.

**Example: Reading and Writing Files**
```go
package main

import (
	"fmt"
	"os"
)

func main() {
	// Write to a file
	data := []byte("Hello, Go standard library!")
	err := os.WriteFile("example.txt", data, 0644)
	if err != nil {
		fmt.Println("Error writing file:", err)
		return
	}
	fmt.Println("File written successfully")

	// Read from a file
	content, err := os.ReadFile("example.txt")
	if err != nil {
		fmt.Println("Error reading file:", err)
		return
	}
	fmt.Println("File content:", string(content))
}
```

**Output:**
```
File written successfully
File content: Hello, Go standard library!
```

---

## 3. Networking

### net/http Package
The `net/http` package provides HTTP client and server implementations.

**Example: HTTP Server**
```go
package main

import (
	"fmt"
	"net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello, Go HTTP Server!")
}

func main() {
	http.HandleFunc("/", handler)
	fmt.Println("Server starting at http://localhost:8080")
	http.ListenAndServe(":8080", nil)
}
```

**Run the code** and visit [http://localhost:8080](http://localhost:8080).

---

### HTTP Client
**Example: HTTP Client**
```go
package main

import (
	"fmt"
	"io"
	"net/http"
)

func main() {
	resp, err := http.Get("http://127.0.0.1:8080")
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	defer resp.Body.Close()

	body, _ := io.ReadAll(resp.Body)
	fmt.Println(string(body))
}
```

---

## 4. Data Structures

### container/list
Provides a doubly linked list implementation.

**Example: Using `container/list`**
```go
package main

import (
	"container/list"
	"fmt"
)

func main() {
	l := list.New()
	l.PushBack(10)
	l.PushBack(20)
	l.PushFront(5)

	// Iterate through the list
	for e := l.Front(); e != nil; e = e.Next() {
		fmt.Println(e.Value)
	}
}
```

**Output:**
```
5
10
20
```

---

### sort
The `sort` package provides functions for sorting slices.

**Example: Sorting Integers**
```go
package main

import (
	"fmt"
	"sort"
)

func main() {
	numbers := []int{5, 2, 6, 3, 1}
	sort.Ints(numbers)
	fmt.Println("Sorted:", numbers)
}
```

**Output:**
```
Sorted: [1 2 3 5 6]
```

---

## 5. Cryptography

### crypto/md5
Provides MD5 hashing.

**Example: Generate MD5 Hash**
```go
package main

import (
	"crypto/md5"
	"fmt"
	"io"
)

func main() {
	data := "password123"
	hash := md5.New()
	io.WriteString(hash, data)
	fmt.Printf("MD5 Hash: %x\n", hash.Sum(nil))
}
```

**Output:**
```
MD5 Hash: 482c811da5d5b4bc6d497ffa98491e38
```

---

## 6. JSON Handling

### encoding/json
The `encoding/json` package provides functions to encode and decode JSON data.

**Example: Encode and Decode JSON**
```go
package main

import (
	"encoding/json"
	"fmt"
)

type Person struct {
	Name string `json:"name"`
	Age  int    `json:"age"`
}

func main() {
	// Encode to JSON
	p := Person{Name: "Alice", Age: 30}
	jsonData, _ := json.Marshal(p)
	fmt.Println("JSON:", string(jsonData))

	// Decode from JSON
	var decoded Person
	json.Unmarshal(jsonData, &decoded)
	fmt.Printf("Decoded: %+v\n", decoded)
}
```

**Output:**
```
JSON: {"name":"Alice","age":30}
Decoded: {Name:Alice Age:30}
```

---

## 7. Concurrency

### sync Package
The `sync` package provides primitives for synchronizing goroutines.

**Example: Using WaitGroup**
```go
package main

import (
	"fmt"
	"sync"
)

func worker(id int, wg *sync.WaitGroup) {
	defer wg.Done()
	fmt.Printf("Worker %d starting\n", id)
	fmt.Printf("Worker %d done\n", id)
}

func main() {
	var wg sync.WaitGroup
	for i := 1; i <= 3; i++ {
		wg.Add(1)
		go worker(i, &wg)
	}
	wg.Wait()
	fmt.Println("All workers completed")
}
```

**Output:**
```
Worker 1 starting
Worker 1 done
Worker 2 starting
Worker 2 done
Worker 3 starting
Worker 3 done
All workers completed
```

---

## Best Practices with the Standard Library

1. **Understand Core Packages**: Master frequently used packages like `fmt`, `time`, `os`, and `net/http`.
2. **Leverage Built-in Tools**: Use `sync` for concurrency, `sort` for data structures, and `encoding/json` for JSON handling.
3. **Minimize External Dependencies**: Go’s standard library covers most use cases, ensuring simpler, faster, and more secure applications.
4. **Read the Documentation**: The [Go Documentation](https://pkg.go.dev/std) is an excellent resource to explore package details.

---

## Summary

Go's standard library is a robust collection of packages that cover a wide range of functionality. By understanding and utilizing these packages, you can build powerful and efficient applications with minimal dependencies. From I/O operations and networking to concurrency and cryptography, the standard library provides tools for virtually every common task in software development.