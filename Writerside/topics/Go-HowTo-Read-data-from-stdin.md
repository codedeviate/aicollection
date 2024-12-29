# Reading Data from `stdin` in Go

When writing a utility program that can be used in a pipeline, reading data from `stdin` (standard input) is often required. This allows your program to accept input from other programs or from files, making it more flexible and versatile.

In Go, you can use the `bufio` package to read from `stdin`. The `bufio` package offers buffered I/O operations, which are typically more efficient than reading data directly from `os.Stdin`, especially when handling large inputs or frequent reads.

## Basic Example: Reading and Printing Input

The simplest case is reading input line by line from `stdin` and printing it to the console. This can be done with a `Scanner` from the `bufio` package. Here’s a basic example:

```go
package main

import (
    "bufio"
    "fmt"
    "os"
)

func main() {
    scanner := bufio.NewScanner(os.Stdin)

    for scanner.Scan() {
        fmt.Println("Input:", scanner.Text())
    }

    if err := scanner.Err(); err != nil {
        fmt.Fprintln(os.Stderr, "Error reading from stdin:", err)
    }
}
```

**How it works:**
- We create a `Scanner` that reads from `os.Stdin`.
- A `for` loop continues as long as `scanner.Scan()` returns `true`, meaning that input is available.
- For each line, we print the input using `fmt.Println()`.
- If an error occurs while reading input, we print it to `stderr`.

**Usage examples:**
1. **Interactive input**: You can type some text and press `Enter`. The program will read the input and print it back.
2. **End-of-file (EOF)**: Press `Ctrl+D` (Linux/Mac) or `Ctrl+Z` (Windows) to signal the end of input and terminate the program.
3. **Redirect input from a file**: Run the program with `./program < input.txt` to read from a file instead of typing input manually.
4. **Pipe input from another program**: Use `echo "Hello, World!" | ./program` to pass the output of `echo` as input to your program.

## Enhanced Example: Handling Missing Input and Fallback to a File

A more flexible approach involves checking if any data is available on `stdin`. If there’s no input provided, the program can try reading from a file instead. This is useful if your program can be run both interactively or as part of a pipeline.

```go
package main

import (
    "bufio"
    "fmt"
    "os"
)

func main() {
    scanner := bufio.NewScanner(os.Stdin)

    if !scanner.Scan() {
        if len(os.Args) < 2 {
            fmt.Fprintln(os.Stderr, "No input provided")
            os.Exit(1)
        }

        filename := os.Args[1]
        file, err := os.Open(filename)
        if err != nil {
            fmt.Fprintln(os.Stderr, "Error opening file:", err)
            os.Exit(1)
        }
        defer file.Close()

        scanner = bufio.NewScanner(file)
    }

    for scanner.Scan() {
        fmt.Println("Input:", scanner.Text())
    }

    if err := scanner.Err(); err != nil {
        fmt.Fprintln(os.Stderr, "Error reading input:", err)
    }
}
```

**How it works:**
- If there’s no input on `stdin` (i.e., `scanner.Scan()` returns `false`), the program checks if a filename is provided as a command-line argument.
- If no filename is provided, it reports an error and exits.
- If a filename is provided, it opens the file and reads from it, just like it would from `stdin`.

**Usage examples:**
1. **No input from stdin**: If you don’t type any input, the program will attempt to open the file provided as an argument (e.g., `./program input.txt`).
2. **File input**: If the file doesn’t exist or there’s an issue opening it, the program will display an error message.

## Advanced Example: Checking if Input is from `stdin` or a File

To make the program even more versatile, we can check if the input is coming from `stdin` or from a file by using `os.Stdin.Stat()`. This approach is useful when you want to detect the source of input programmatically and handle each case differently.

```go
package main

import (
    "bufio"
    "fmt"
    "os"
)

func main() {
    stat, _ := os.Stdin.Stat()
    if (stat.Mode() & os.ModeCharDevice) != 0 {
        if len(os.Args) < 2 {
            fmt.Fprintln(os.Stderr, "No input provided")
            os.Exit(1)
        }

        filename := os.Args[1]
        file, err := os.Open(filename)
        if err != nil {
            fmt.Fprintln(os.Stderr, "Error opening file:", err)
            os.Exit(1)
        }
        defer file.Close()

        scanner := bufio.NewScanner(file)

        for scanner.Scan() {
            fmt.Println("Input:", scanner.Text())
        }

        if err := scanner.Err(); err != nil {
            fmt.Fprintln(os.Stderr, "Error reading input:", err)
        }
    } else {
        scanner := bufio.NewScanner(os.Stdin)

        for scanner.Scan() {
            fmt.Println("Input:", scanner.Text())
        }

        if err := scanner.Err(); err != nil {
            fmt.Fprintln(os.Stderr, "Error reading input:", err)
        }
    }
}
```

**How it works:**
- We check the mode of `os.Stdin` using `os.Stdin.Stat()`. If `stdin` is a terminal (a character device), it means there’s no data piped into the program.
- If `stdin` is not connected to a terminal, the program falls back to reading from a file provided as an argument.
- This approach allows the program to dynamically handle different input sources: `stdin` for interactive or piped input, and a file for redirected input.

**Usage examples:**
1. **Interactive or piped input**: When `stdin` is connected to a terminal or another program via a pipe, the program will read from `stdin`.
2. **File input**: When `stdin` is not connected to a terminal (i.e., input is redirected), the program reads from the provided file.

---

With these examples, you now have a program capable of handling various types of input sources: interactive user input, piped data from other programs, and file input. By leveraging Go’s `bufio` package and `os.Stdin.Stat()`, you can create highly flexible command-line utilities.