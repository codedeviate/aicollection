# Netscan

To create a network scan program in Go, you need to create a few files: `main.go` for the main logic, and optionally, a `netscan.go` file for the network scanning functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir netscan
cd netscan
go mod init github.com/username/netscan
```

## Step 2: Create the `netscan.go` File

Create a `netscan.go` file to handle the network scanning functionality.

```go
// netscan.go
package main

import (
    "fmt"
    "net"
    "time"
)

// ScanPort checks if a port is open on a given host.
func ScanPort(protocol, hostname string, port int) bool {
    address := fmt.Sprintf("%s:%d", hostname, port)
    conn, err := net.DialTimeout(protocol, address, time.Second)
    if err != nil {
        return false
    }
    conn.Close()
    return true
}

// ScanHost scans a range of ports on a given host.
func ScanHost(hostname string, startPort, endPort int) {
    for port := startPort; port <= endPort; port++ {
        if ScanPort("tcp", hostname, port) {
            fmt.Printf("Port %d is open\n", port)
        }
    }
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the network scanning functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
    "strconv"
)

func main() {
    if len(os.Args) != 4 {
        fmt.Println("Usage: netscan <hostname> <startPort> <endPort>")
        os.Exit(1)
    }

    hostname := os.Args[1]
    startPort, err := strconv.Atoi(os.Args[2])
    if err != nil {
        fmt.Printf("Invalid start port: %v\n", err)
        os.Exit(1)
    }

    endPort, err := strconv.Atoi(os.Args[3])
    if err != nil {
        fmt.Printf("Invalid end port: %v\n", err)
        os.Exit(1)
    }

    ScanHost(hostname, startPort, endPort)
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go example.com 1 1024
```

This will scan ports 1 to 1024 on the specified hostname and output the open ports.