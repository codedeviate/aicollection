# Port Forwarding

To create a port forwarding program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `forwarder.go` file for the port forwarding functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir portforwarding
cd portforwarding
go mod init github.com/username/portforwarding
```

## Step 2: Create the `forwarder.go` File

Create a `forwarder.go` file to handle the port forwarding functionality.

```go
// forwarder.go
package main

import (
    "io"
    "log"
    "net"
)

// forward handles the forwarding of data between the client and the target server.
func forward(src net.Conn, dst net.Conn) {
    defer src.Close()
    defer dst.Close()
    io.Copy(src, dst)
}

// handleConnection handles the incoming client connection and forwards data to the target server.
func handleConnection(clientConn net.Conn, target string) {
    defer clientConn.Close()

    serverConn, err := net.Dial("tcp", target)
    if err != nil {
        log.Printf("Failed to connect to target server: %v", err)
        return
    }
    defer serverConn.Close()

    go forward(clientConn, serverConn)
    forward(serverConn, clientConn)
}

// StartForwarder starts the port forwarder on the specified port and forwards traffic to the target server.
func StartForwarder(listenPort, target string) error {
    listener, err := net.Listen("tcp", ":"+listenPort)
    if err != nil {
        return err
    }
    defer listener.Close()

    log.Printf("Port forwarder started on port %s, forwarding to %s", listenPort, target)
    for {
        clientConn, err := listener.Accept()
        if err != nil {
            log.Printf("Failed to accept connection: %v", err)
            continue
        }
        go handleConnection(clientConn, target)
    }
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the port forwarding functionality.

```go
// main.go
package main

import (
    "fmt"
    "log"
    "os"
)

func main() {
    if len(os.Args) != 3 {
        fmt.Println("Usage: portforwarding <listen_port> <target>")
        os.Exit(1)
    }

    listenPort := os.Args[1]
    target := os.Args[2]

    fmt.Printf("Starting port forwarder on port %s, forwarding to %s...\n", listenPort, target)
    if err := StartForwarder(listenPort, target); err != nil {
        log.Fatalf("Port forwarder failed: %v", err)
    }
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go 8080 example.com:80
```

This will start the port forwarder on port 8080 and forward traffic to `example.com` on port 80.