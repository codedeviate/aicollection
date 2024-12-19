# Create a module

To create a Go module, you need to follow these steps:

1. **Initialize a new module**: Use the `go mod init` command to create a new module.
2. **Create packages**: Organize your code into packages.
3. **Use the module**: Import and use the packages within your module.

Here are detailed examples:

## Step 1: Initialize a New Module

First, create a new directory for your project and navigate into it. Then, initialize the module.

```sh
mkdir mymodule
cd mymodule
go mod init github.com/username/mymodule
```

## Step 2: Create Packages

Create a directory structure for your packages. For example, create two packages: `math` and `stringutil`.

```sh
mkdir -p math stringutil
```

### Example: `math` Package

Create a file `math/math.go`:

```go
package math

// Add adds two integers and returns the result.
func Add(a, b int) int {
    return a + b
}
```

### Example: `stringutil` Package

Create a file `stringutil/stringutil.go`:

```go
package stringutil

// Reverse returns the reverse of the given string.
func Reverse(s string) string {
    runes := []rune(s)
    for i, j := 0, len(runes)-1; i < j; i, j = i+1, j-1 {
        runes[i], j = runes[j], runes[i]
    }
    return string(runes)
}
```

## Step 3: Use the Module

Create a `main.go` file in the root directory to use the packages.

```go
package main

import (
    "fmt"
    "github.com/username/mymodule/math"
    "github.com/username/mymodule/stringutil"
)

func main() {
    // Use the math package
    sum := math.Add(3, 4)
    fmt.Println("Sum:", sum)

    // Use the stringutil package
    reversed := stringutil.Reverse("hello")
    fmt.Println("Reversed:", reversed)
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go
```

This will output:

```
Sum: 7
Reversed: olleh
```

By following these steps, you can create a Go module with multiple packages and use them in your project.