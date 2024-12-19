# Proxy Server

To create a proxy server program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `proxy.go` file for the proxy server functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir proxyserver
cd proxyserver
go mod init github.com/username/proxyserver
```

## Step 2: Create the `proxy.go` File

Create a `proxy.go` file to handle the proxy server functionality.

```go
// proxy.go
package main

import (
    "io"
    "log"
    "net"
)

// handleConnection handles the incoming client connection and forwards data to the target server.
func handleConnection(clientConn net.Conn, target string) {
    defer clientConn.Close()

    serverConn, err := net.Dial("tcp", target)
    if err != nil {
        log.Printf("Failed to connect to target server: %v", err)
        return
    }
    defer serverConn.Close()

    go io.Copy(serverConn, clientConn)
    io.Copy(clientConn, serverConn)
}

// StartProxy starts the proxy server on the specified port and forwards traffic to the target server.
func StartProxy(listenPort, target string) error {
    listener, err := net.Listen("tcp", ":"+listenPort)
    if err != nil {
        return err
    }
    defer listener.Close()

    log.Printf("Proxy server started on port %s, forwarding to %s", listenPort, target)
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

Create a `main.go` file to use the proxy server functionality.

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
        fmt.Println("Usage: proxyserver <listen_port> <target>")
        os.Exit(1)
    }

    listenPort := os.Args[1]
    target := os.Args[2]

    fmt.Printf("Starting proxy server on port %s, forwarding to %s...\n", listenPort, target)
    if err := StartProxy(listenPort, target); err != nil {
        log.Fatalf("Proxy server failed: %v", err)
    }
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go 8080 example.com:80
```

This will start the proxy server on port 8080 and forward traffic to `example.com` on port 80.