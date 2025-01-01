# Hello, World

Here is a simple "Hello World" program in Go:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

## Steps to Compile and Build

1. **Save the code**: Save the above code in a file named `hello.go`.

2. **Open a terminal**: Navigate to the directory where `hello.go` is saved.

3. **Compile the code**: Use the `go` command to compile the code. Run the following command:
   ```sh
   go build hello.go
   ```

4. **Run the executable**: After compilation, an executable file named `hello` (or `hello.exe` on Windows) will be created. Run it using:
   ```sh
   ./hello
   ```

This will output:
```
Hello, World!
```