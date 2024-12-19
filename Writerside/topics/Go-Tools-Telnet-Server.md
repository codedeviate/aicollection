# Telnet Server

To create a Telnet server program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `server.go` file for the server functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir telnetserver
cd telnetserver
go mod init github.com/username/telnetserver
```

## Step 2: Create the `server.go` File

Create a `server.go` file to handle the Telnet server functionality.

```go
// server.go
package main

import (
    "bufio"
    "fmt"
    "net"
    "strings"
)

// handleConnection handles incoming Telnet connections.
func handleConnection(conn net.Conn) {
    defer conn.Close()
    reader := bufio.NewReader(conn)
    for {
        conn.Write([]byte("> "))
        input, err := reader.ReadString('\n')
        if err != nil {
            return
        }
        input = strings.TrimSpace(input)
        if input == "exit" {
            return
        }
        response := fmt.Sprintf("You said: %s\n", input)
        conn.Write([]byte(response))
    }
}

// StartServer starts the Telnet server on the specified port.
func StartServer(port string) error {
    listener, err := net.Listen("tcp", ":"+port)
    if err != nil {
        return err
    }
    defer listener.Close()
    fmt.Printf("Telnet server started on port %s\n", port)
    for {
        conn, err := listener.Accept()
        if err != nil {
            return err
        }
        go handleConnection(conn)
    }
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the server functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: telnetserver <port>")
        os.Exit(1)
    }

    port := os.Args[1]
    fmt.Printf("Starting Telnet server on port %s...\n", port)
    if err := StartServer(port); err != nil {
        fmt.Printf("Server failed: %v\n", err)
        os.Exit(1)
    }
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go 2323
```

This will start the Telnet server on port 2323. You can connect to it using a Telnet client.