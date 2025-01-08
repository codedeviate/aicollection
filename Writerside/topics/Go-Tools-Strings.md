# Strings

## Building a Modular `strings` Command in Go

The `strings` command in Unix-based systems extracts printable strings from binary files. This functionality is useful for analyzing and extracting human-readable text from files that contain mostly binary data. In this article, we will walk through creating a Go program that mimics this functionality while adhering to the principles of modular design. The code will be organized into multiple directories, allowing for better maintainability and extendability.

### Project Overview

The goal of this project is to create a simple Go program that extracts printable strings from a binary file. The program will:
1. Take the file path as input.
2. Read the file in chunks.
3. Extract sequences of printable ASCII characters.
4. Print all extracted strings longer than a specified threshold.

We will structure the program into three core parts:
- **Main program** (`main.go`): Entry point.
- **Extractor module** (`extractor/extractor.go`): Core logic for extracting strings.
- **Utilities module** (`utils/utils.go`): Helper functions, such as checking if a character is printable.

### Project Structure

```
strings/
│
├── main.go              // Entry point of the program
├── extractor/           // Module to extract strings
│   └── extractor.go     // Logic to read file and extract strings
└── utils/               // Utility functions
    └── utils.go         // Helper functions (e.g., isPrintable)
```

### Step-by-Step Guide

#### 1. Initialize the Go Project

The first step in setting up the project is to initialize the Go module. This will create the `go.mod` file to manage dependencies.

```bash
go mod init strings
```

This will create the Go module, and you can now start organizing the code into different files and directories.

#### 2. Extractor Module: `extractor/extractor.go`

The `extractor/extractor.go` module is responsible for the core functionality of extracting printable strings from a binary file.

```go
// extractor/extractor.go
package extractor

import (
	"os"

	"github.com/username/strings/utils"
)

// Minimum length of printable strings to extract
const MinStringLength = 4

// ExtractStrings reads a file and returns a slice of printable strings.
func ExtractStrings(filePath string) ([]string, error) {
	file, err := os.Open(filePath)
	if err != nil {
		return nil, err
	}
	defer file.Close()

	var result []string
	var currentString []byte

	buf := make([]byte, 4096) // Buffer size
	for {
		n, err := file.Read(buf)
		if err != nil && err.Error() != "EOF" {
			return nil, err
		}

		// Process bytes in the buffer
		for i := 0; i < n; i++ {
			c := buf[i]
			if utils.IsPrintable(c) {
				currentString = append(currentString, c)
			} else {
				if len(currentString) >= MinStringLength {
					result = append(result, string(currentString))
				}
				currentString = nil
			}
		}

		// Break if we reached EOF
		if err != nil {
			break
		}
	}

	// Add any remaining string after the loop
	if len(currentString) >= MinStringLength {
		result = append(result, string(currentString))
	}

	return result, nil
}

```

##### Explanation (extractor.go):
- **`MinStringLength`**: This constant determines the minimum length of strings that are extracted. Strings shorter than this length are ignored.
- **`isPrintable` function**: This helper function checks if a byte is a printable ASCII character. It uses the `unicode` package to check if the character is printable and not a control character.
- **`ExtractStrings` function**: This function opens the file, reads it in chunks (using a buffer), and extracts all printable strings longer than the threshold. The result is a slice of strings.

#### 3. Utilities Module: `utils/utils.go`

The utilities module contains helper functions like `isPrintable` to check for printable characters.

```go
// utils/utils.go
package utils

import "unicode"

// isPrintable checks if a byte is a printable ASCII character.
func IsPrintable(c byte) bool {
	return unicode.IsPrint(rune(c)) && !unicode.IsControl(rune(c))
}

```

Although we have already implemented `isPrintable` inside the `extractor` module, splitting it into a separate `utils` package makes the code more reusable across different parts of the application.

#### 4. Main Program: `main.go`

The `main.go` file is the entry point of the program. It will handle the command-line argument, call the `extractStrings` function, and print the results.

```go
// main.go
package main

import (
	"fmt"
	"os"

	"github.com/username/strings/extractor"
)

func main() {
	if len(os.Args) < 2 {
		fmt.Println("Usage: go run main.go <filename>")
		os.Exit(1)
	}

	filePath := os.Args[1]
	strings, err := extractor.ExtractStrings(filePath)
	if err != nil {
		fmt.Println("Error:", err)
		os.Exit(1)
	}

	for _, s := range strings {
		fmt.Println(s)
	}
}

```

##### Explanation (main.go):
- The `main.go` file reads the file path from the command-line argument, calls the `extractStrings` function from the `extractor` module, and prints the extracted strings to standard output.
- If the file path is not provided or an error occurs while reading the file, the program exits with a helpful error message.

### Running the Program

Once all the modules are implemented, you can build and run the program. Here's how you can do it:

1. **Run the Program**:
   ```bash
   go run main.go <file-path>
   ```

2. **Expected Output**:
   The program will print all printable strings from the binary file that are at least 4 characters long.

### Example

Consider a binary file `example.bin` that contains some human-readable text. You would run the program like this:

```bash
go run main.go example.bin
```

The output might look like this:

```
Hello, World!
This is a test string.
Another example.
```

### Conclusion

This Go program mimics the functionality of the Unix `strings` command by extracting printable strings from a binary file. We have structured the code into separate modules for maintainability and flexibility:
- **`main.go`**: Handles program execution and user input.
- **`extractor/extractor.go`**: Contains the core logic for extracting strings.
- **`utils/utils.go`**: Provides utility functions like checking if a character is printable.

This modular structure allows you to easily expand and maintain the code in the future, such as adding new features or improving performance.