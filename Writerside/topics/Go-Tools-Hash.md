# Hash

To create a hash utility program in Go that supports all major hash algorithms, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir hash_utility
cd hash_utility
go mod init github.com/username/hash_utility
```

## Step 2: Create the `hash.go` File

Create a `hash.go` file to handle the hashing functionality.

```go
// hash.go
package main

import (
    "crypto/md5"
    "crypto/sha1"
    "crypto/sha256"
    "crypto/sha512"
    "encoding/hex"
    "fmt"
    "hash"
    "io"
    "os"
)

// HashData hashes the input data using the specified hash algorithm.
func HashData(data string, algorithm string) (string, error) {
    var hasher hash.Hash

    switch algorithm {
    case "md5":
        hasher = md5.New()
    case "sha1":
        hasher = sha1.New()
    case "sha256":
        hasher = sha256.New()
    case "sha512":
        hasher = sha512.New()
    default:
        return "", fmt.Errorf("unsupported hash algorithm: %s", algorithm)
    }

    _, err := hasher.Write([]byte(data))
    if err != nil {
        return "", err
    }

    return hex.EncodeToString(hasher.Sum(nil)), nil
}

// HashFile hashes the content of the specified file using the specified hash algorithm.
func HashFile(filePath string, algorithm string) (string, error) {
    file, err := os.Open(filePath)
    if err != nil {
        return "", err
    }
    defer file.Close()

    var hasher hash.Hash

    switch algorithm {
    case "md5":
        hasher = md5.New()
    case "sha1":
        hasher = sha1.New()
    case "sha256":
        hasher = sha256.New()
    case "sha512":
        hasher = sha512.New()
    default:
        return "", fmt.Errorf("unsupported hash algorithm: %s", algorithm)
    }

    if _, err := io.Copy(hasher, file); err != nil {
        return "", err
    }

    return hex.EncodeToString(hasher.Sum(nil)), nil
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the hashing functionality.

```go
package main

import (
    "bufio"
    "flag"
    "fmt"
    "io"
    "os"
)

func main() {
    algorithm := flag.String("algorithm", "sha256", "Hash algorithm: md5, sha1, sha256, sha512")
    input := flag.String("input", "", "Input string")
    filePath := flag.String("file", "", "Path to input file")
    flag.Parse()

    var data string
    if *filePath != "" {
        // Read from file
        result, err := HashFile(*filePath, *algorithm)
        if err != nil {
            fmt.Printf("Error hashing file: %v\n", err)
            os.Exit(1)
        }
        fmt.Println(result)
        return
    } else if *input == "" {
        // Check if input is coming from a pipe
        fi, err := os.Stdin.Stat()
        if err != nil {
            fmt.Printf("Error: %v\n", err)
            os.Exit(1)
        }

        if fi.Mode()&os.ModeNamedPipe != 0 {
            // Read from stdin
            reader := bufio.NewReader(os.Stdin)
            inputBytes, err := io.ReadAll(reader)
            if err != nil {
                fmt.Printf("Error reading from stdin: %v\n", err)
                os.Exit(1)
            }
            data = string(inputBytes)
        } else {
            fmt.Println("Enter input string:")
            scanner := bufio.NewScanner(os.Stdin)
            if scanner.Scan() {
                data = scanner.Text()
            }
        }
    } else {
        data = *input
    }

    result, err := HashData(data, *algorithm)
    if err != nil {
        fmt.Printf("Error hashing data: %v\n", err)
        os.Exit(1)
    }

    fmt.Println(result)
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

To hash a string using SHA-256:

```sh
go run main.go --algorithm sha256 --input "Hello, World!"
```

To hash a file using SHA-256:

```sh
go run main.go --algorithm sha256 --file path/to/input.txt
```

To hash data piped from another command using SHA-256:

```sh
echo "Hello, World!" | go run main.go --algorithm sha256
```

This will hash the input data based on the specified algorithm.