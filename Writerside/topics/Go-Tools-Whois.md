# Whois

To create a Whois program in Go, you need to create a few files: `main.go` for the main logic, and optionally, a `whois.go` file for the Whois functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir whois
cd whois
go mod init github.com/username/whois
```

## Step 2: Create the `whois.go` File

Create a `whois.go` file to handle the Whois functionality.

```go
// whois.go
package main

import (
    "bufio"
    "fmt"
    "net"
    "strings"
    "time"
)

// Whois performs a whois query for the given domain and returns the result.
func Whois(domain string) (string, error) {
    conn, err := net.DialTimeout("tcp", "whois.verisign-grs.com:43", time.Second*10)
    if err != nil {
        return "", err
    }
    defer conn.Close()

    fmt.Fprintf(conn, "%s\r\n", domain)
    scanner := bufio.NewScanner(conn)
    var result strings.Builder
    for scanner.Scan() {
        result.WriteString(scanner.Text() + "\n")
    }
    if err := scanner.Err(); err != nil {
        return "", err
    }
    return result.String(), nil
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the Whois functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: whois <domain>")
        os.Exit(1)
    }

    domain := os.Args[1]
    result, err := Whois(domain)
    if err != nil {
        fmt.Printf("Whois query for %s failed: %v\n", domain, err)
        os.Exit(1)
    }

    fmt.Printf("Whois result for %s:\n%s", domain, result)
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go example.com
```

This will output the Whois information for the specified domain.