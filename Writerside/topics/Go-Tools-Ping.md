# Ping

To create a ping program in Go, you need to create a few files: `main.go` for the main logic, and optionally, a `ping.go` file for the ping functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir ping
cd ping
go mod init github.com/username/ping
mkdir pingmod
```

## Step 2: Create the `ping.go` File

Create a `ping.go` file in the `pingmod` directory to handle the ping functionality.

```go
// ping.go
package ping

import (
	"net"
	"time"
)

// Ping sends a ping request to the specified address and returns the duration and any error encountered.
func Ping(address string) (time.Duration, error) {
    start := time.Now()
    conn, err := net.DialTimeout("ip4:icmp", address, time.Second*2)
    if err != nil {
        return 0, err
    }
    defer conn.Close()
    duration := time.Since(start)
    return duration, nil
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the ping functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
    "github.com/username/ping/pingmod"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: ping <address>")
        os.Exit(1)
    }

    address := os.Args[1]
    duration, err := Ping(address)
    if err != nil {
        fmt.Printf("Ping to %s failed: %v\n", address, err)
        os.Exit(1)
    }

    fmt.Printf("Ping to %s: %v\n", address, duration)
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go google.com
```

This will output the ping duration to the specified address.