# Port Scanner

To create a port scanner program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `scanner.go` file for the scanning functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir portscanner
cd portscanner
go mod init github.com/username/portscanner
```

## Step 2: Create the `scanner.go` File

Create a `scanner/portscanner.go` file to handle the port scanning functionality.

```go
// portscanner.go
package portscanner

import (
	"fmt"
	"net"
	"time"
)

// ScanPort checks if a port is open on a given host.
func ScanPort(protocol, hostname string, port int) bool {
	address := fmt.Sprintf("%s:%d", hostname, port)
	conn, err := net.DialTimeout(protocol, address, 1*time.Second)
	if err != nil {
		return false
	}
	conn.Close()
	return true
}

// ScanPorts scans a range of ports on a given host.
func ScanPorts(protocol, hostname string, startPort, endPort int) []int {
	var openPorts []int
	for port := startPort; port <= endPort; port++ {
		if ScanPort(protocol, hostname, port) {
			openPorts = append(openPorts, port)
		}
	}
	return openPorts
}

```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the scanning functionality.

```go
// main.go
package main

import (
	"fmt"
	"os"
	"strconv"

	portscanner "github.com/username/portscanner/scanner"
)

func main() {
	if len(os.Args) != 5 {
		fmt.Println("Usage: portscanner <protocol> <hostname> <startPort> <endPort>")
		os.Exit(1)
	}

	protocol := os.Args[1]
	hostname := os.Args[2]
	startPort, err := strconv.Atoi(os.Args[3])
	if err != nil {
		fmt.Printf("Invalid start port: %v\n", err)
		os.Exit(1)
	}
	endPort, err := strconv.Atoi(os.Args[4])
	if err != nil {
		fmt.Printf("Invalid end port: %v\n", err)
		os.Exit(1)
	}

	openPorts := portscanner.ScanPorts(protocol, hostname, startPort, endPort)
	if len(openPorts) == 0 {
		fmt.Println("No open ports found.")
	} else {
		fmt.Printf("Open ports: %v\n", openPorts)
	}
}

```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go tcp example.com 1 1024
```

This will scan the ports from 1 to 1024 on the specified host using the specified protocol and print the open ports.