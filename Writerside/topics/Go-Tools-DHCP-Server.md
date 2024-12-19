# DHCP Server

To create a DHCP server program in Go, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir dhcpserver
cd dhcpserver
go mod init github.com/username/dhcpserver
```

## Step 2: Install Dependencies

You will need the `insomniacslk/dhcp` library for DHCP server functionality.

```sh
go get github.com/insomniacslk/dhcp
```

## Step 3: Create the `dhcpserver.go` File

Create a `dhcpserver.go` file to handle the DHCP server functionality.

```go
// dhcpserver.go
package main

import (
    "github.com/insomniacslk/dhcp/dhcpv4"
    "github.com/insomniacslk/dhcp/dhcpv4/server4"
    "log"
    "net"
)

// handleDHCPRequest handles incoming DHCP requests.
func handleDHCPRequest(conn net.PacketConn, peer net.Addr, req *dhcpv4.DHCPv4) {
    log.Printf("Received DHCP request from %v", peer)

    // Create a DHCP offer packet
    offer, err := dhcpv4.New()
    if err != nil {
        log.Printf("Failed to create DHCP offer: %v", err)
        return
    }

    offer.OpCode = dhcpv4.OpcodeBootReply
    offer.YourIPAddr = net.IPv4(192, 168, 1, 100) // Example IP address
    offer.ServerIPAddr = net.IPv4(192, 168, 1, 1) // Example server IP address
    offer.BootFileName = "bootfile"

    // Send the DHCP offer
    if _, err := conn.WriteTo(offer.ToBytes(), peer); err != nil {
        log.Printf("Failed to send DHCP offer: %v", err)
    }
}

// StartDHCPServer starts the DHCP server on the specified interface.
func StartDHCPServer(iface string) {
    handler := server4.HandlerFunc(handleDHCPRequest)
    server, err := server4.NewServer(iface, nil, handler)
    if err != nil {
        log.Fatalf("Failed to start DHCP server: %v", err)
    }

    log.Printf("Starting DHCP server on interface %s", iface)
    if err := server.Serve(); err != nil {
        log.Fatalf("Failed to serve: %v", err)
    }
}
```

## Step 4: Create the `main.go` File

Create a `main.go` file to use the DHCP server functionality.

```go
// main.go
package main

import (
    "fmt"
    "log"
    "os"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: dhcpserver <network_interface>")
        os.Exit(1)
    }

    iface := os.Args[1]

    fmt.Printf("Starting DHCP server on interface %s...\n", iface)
    StartDHCPServer(iface)
}
```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go <network_interface>
```

Replace `<network_interface>` with the name of the network interface you want to use (e.g., `eth0` on Linux or `en0` on macOS). This will start the DHCP server on the specified network interface.