# Dig/nslookup

To create a `dig/nslookup` program in Go, you need to create a few files: `main.go` for the main logic, and optionally, a `dnslookup.go` file for the DNS lookup functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir dnslookup
cd dnslookup
go mod init github.com/username/dnslookup
```

## Step 2: Create the `dnslookup.go` File

Create a `dnslookup.go` file to handle the DNS lookup functionality.

```go
// dnslookup.go
package main

import (
    "fmt"
    "net"
)

// DNSLookup performs a DNS lookup for the given domain and returns the IP addresses.
func DNSLookup(domain string) ([]string, error) {
    ips, err := net.LookupIP(domain)
    if err != nil {
        return nil, err
    }
    var result []string
    for _, ip := range ips {
        result.append(result, ip.String())
    }
    return result, nil
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the DNS lookup functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: dnslookup <domain>")
        os.Exit(1)
    }

    domain := os.Args[1]
    ips, err := DNSLookup(domain)
    if err != nil {
        fmt.Printf("DNS lookup for %s failed: %v\n", domain, err)
        os.Exit(1)
    }

    fmt.Printf("DNS lookup result for %s:\n", domain)
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

This will output the IP addresses for the specified domain.