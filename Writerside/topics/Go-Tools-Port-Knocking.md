# Port Knocking

To create a port knocking program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `knock.go` file for the port knocking functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir portknocking
cd portknocking
go mod init github.com/username/portknocking
```

## Step 2: Create the `knock.go` File

Create a `knock.go` file to handle the port knocking functionality.

```go
// knock.go
package main

import (
    "fmt"
    "net"
    "time"
)

// Knock sends a sequence of packets to the specified ports.
func Knock(host string, ports []int, delay time.Duration) error {
    for _, port := range ports {
        address := fmt.Sprintf("%s:%d", host, port)
        conn, err := net.Dial("udp", address)
        if err != nil {
            return err
        }
        conn.Close()
        time.Sleep(delay)
    }
    return nil
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the port knocking functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
    "strconv"
    "time"
)

func main() {
    if len(os.Args) < 4 {
        fmt.Println("Usage: portknocking <host> <delay_ms> <port1> <port2> ... <portN>")
        os.Exit(1)
    }

    host := os.Args[1]
    delayMs, err := strconv.Atoi(os.Args[2])
    if err != nil {
        fmt.Printf("Invalid delay: %v\n", err)
        os.Exit(1)
    }
    delay := time.Duration(delayMs) * time.Millisecond

    var ports []int
    for _, arg := range os.Args[3:] {
        port, err := strconv.Atoi(arg)
        if err != nil {
            fmt.Printf("Invalid port: %v\n", err)
            os.Exit(1)
        }
        ports = append(ports, port)
    }

    if err := Knock(host, ports, delay); err != nil {
        fmt.Printf("Port knocking failed: %v\n", err)
        os.Exit(1)
    }

    fmt.Println("Port knocking sequence completed.")
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go example.com 500 1234 5678 91011
```

This will send a port knocking sequence to `example.com` with a 500ms delay between each knock on ports 1234, 5678, and 91011.