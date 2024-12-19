# Telnet Client

To create a Telnet client program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `client.go` file for the client functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir telnetclient
cd telnetclient
go mod init github.com/username/telnetclient
```

## Step 2: Create the `client.go` File

Create a `client.go` file to handle the Telnet client functionality.

```go
// client.go
package main

import (
    "bufio"
    "fmt"
    "net"
    "os"
)

// ConnectToServer connects to the Telnet server and handles communication.
func ConnectToServer(address string) error {
    conn, err := net.Dial("tcp", address)
    if err != nil {
        return err
    }
    defer conn.Close()

    go func() {
        scanner := bufio.NewScanner(conn)
        for scanner.Scan() {
            fmt.Println(scanner.Text())
        }
    }()

    scanner := bufio.NewScanner(os.Stdin)
    for scanner.Scan() {
        _, err := fmt.Fprintf(conn, "%s\n", scanner.Text())
        if err != nil {
            return err
        }
    }

    return scanner.Err()
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the client functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: telnetclient <address>")
        os.Exit(1)
    }

    address := os.Args[1]
    fmt.Printf("Connecting to Telnet server at %s...\n", address)
    if err := ConnectToServer(address); err != nil {
        fmt.Printf("Connection failed: %v\n", err)
        os.Exit(1)
    }
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go localhost:2323
```

This will connect the Telnet client to the server running on `localhost` at port `2323`. You can interact with the server through the client.