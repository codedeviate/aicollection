# Traceroute

To create a traceroute program in Go, you need to create a few files: `main.go` for the main logic, and optionally, a `traceroute.go` file for the traceroute functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir traceroute
cd traceroute
go mod init github.com/username/traceroute
```

## Step 2: Create the `traceroute.go` File

Create a `traceroute.go` file to handle the traceroute functionality.

```go
// traceroute.go
package main

import (
    "fmt"
    "net"
    "time"
)

// Traceroute performs a traceroute to the specified address.
func Traceroute(address string, maxHops int) ([]string, error) {
    var hops []string
    for ttl := 1; ttl <= maxHops; ttl++ {
        start := time.Now()
        conn, err := net.DialTimeout("ip4:icmp", address, time.Second*2)
        if err != nil {
            return nil, err
        }
        conn.SetTTL(ttl)
        defer conn.Close()

        duration := time.Since(start)
        hops = append(hops, fmt.Sprintf("Hop %d: %v", ttl, duration))
    }
    return hops, nil
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the traceroute functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: traceroute <address>")
        os.Exit(1)
    }

    address := os.Args[1]
    maxHops := 30
    hops, err := Traceroute(address, maxHops)
    if err != nil {
        fmt.Printf("Traceroute to %s failed: %v\n", address, err)
        os.Exit(1)
    }

    fmt.Printf("Traceroute to %s:\n", address)
    for _, hop := range hops {
        fmt.Println(hop)
    }
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go example.com
```

This will output the traceroute hops to the specified address.