# IfInfo

To create a program in Go that lists all available network interfaces and their IP addresses, you need to create a few files: `main.go` for the main logic, and optionally, a `interfaces.go` file for the interface-handling functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir ifinfo
cd ifinfo
mkdir lib
go mod init github.com/username/ifinfo
```

## Step 2: Create the `interfaces.go` File

Create a `interfaces.go` file in the `lib` directory to handle the functionality of listing network interfaces.

```go
package lib

import (
	"fmt"
	"net"
)

// ListInterfaces retrieves all network interfaces and their IP addresses.
func ListInterfaces() {
	interfaces, err := net.Interfaces()
	if err != nil {
		fmt.Printf("Error retrieving interfaces: %v\n", err)
		return
	}

	fmt.Println("Available Network Interfaces:")
	for _, iface := range interfaces {
		fmt.Printf("Name: %s, MTU: %d, HardwareAddr: %s, Flags: %s\n", iface.Name, iface.MTU, iface.HardwareAddr, iface.Flags)

		addrs, err := iface.Addrs()
		if err != nil {
			fmt.Printf("  Error retrieving addresses: %v\n", err)
			continue
		}

		for _, addr := range addrs {
			fmt.Printf("  Address: %s\n", addr.String())
		}
		fmt.Println()
	}
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the network interface listing functionality.

```go
package main

import (
	"github.com/username/ifinfo/lib"
)

func main() {
	lib.ListInterfaces()
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go
```

The program will retrieve and display:
1. All available network interfaces on the system.
2. The associated IP addresses for each interface.

### Example Output

For a machine with several interfaces:
```
Available Network Interfaces:
Name: lo
  Address: 127.0.0.1/8
  Address: ::1/128

Name: eth0
  Address: 192.168.1.100/24
  Address: fe80::1a2b:3c4d:5e6f:7g8h/64

Name: wlan0
  Address: 10.0.0.100/24
  Address: fe80::1234:5678:abcd:ef12/64
```

### Notes
- The program uses the `net` package, which provides tools to list interfaces and their details.
- IP addresses include both IPv4 and IPv6, displayed with their subnet masks.
- If an interface has no assigned IP address, it will still be listed, but without any associated address output.

### Extensions
- You can modify the program to filter interfaces (e.g., only show interfaces with an active connection or only display IPv4 addresses).
- Add error handling to improve robustness in environments with unusual network configurations.