# DNS Client

To create a DNS client program in Go, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir dnsclient
cd dnsclient
go mod init github.com/username/dnsclient
```

## Step 2: Create the `dnsclient.go` File

Create a `dnsclient.go` file to handle the DNS client functionality.

```go
// dnsclient.go
package main

import (
    "fmt"
    "net"
)

// ResolveDNS resolves the given hostname to its IP addresses.
func ResolveDNS(hostname string) ([]net.IP, error) {
    ips, err := net.LookupIP(hostname)
    if err != nil {
        return nil, err
    }
    return ips, nil
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the DNS client functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: dnsclient <hostname>")
        os.Exit(1)
    }

    hostname := os.Args[1]
    ips, err := ResolveDNS(hostname)
    if err != nil {
        fmt.Printf("Failed to resolve DNS: %v\n", err)
        os.Exit(1)
    }

    fmt.Printf("IP addresses for %s:\n", hostname)
    for _, ip := range ips {
        fmt.Println(ip)
    }
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go example.com
```

This will resolve the DNS for `example.com` and print its IP addresses.