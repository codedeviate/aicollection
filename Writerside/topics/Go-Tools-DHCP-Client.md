# DHCP Client

To create a DHCP client program in Go, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir dhcpclient
cd dhcpclient
go mod init github.com/username/dhcpclient
```

## Step 2: Install Dependencies

You will need the `insomniacslk/dhcp` library for DHCP client functionality.

```sh
go get github.com/insomniacslk/dhcp
```

## Step 3: Create the `dhcpclient.go` File

Create a `dhcpclient.go` file to handle the DHCP client functionality.

```go
// dhcpclient.go
package main

import (
    "context"
    "fmt"
    "github.com/insomniacslk/dhcp/dhcpv4"
    "github.com/insomniacslk/dhcp/dhcpv4/nclient4"
    "log"
    "net"
    "time"
)

// RequestIP requests an IP address from a DHCP server.
func RequestIP(iface string) (*dhcpv4.DHCPv4, error) {
    client, err := nclient4.New(iface, nclient4.WithTimeout(10*time.Second))
    if err != nil {
        return nil, err
    }
    defer client.Close()

    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()

    packet, err := client.DiscoverOffer(ctx)
    if err != nil {
        return nil, err
    }

    return packet, nil
}
```

## Step 4: Create the `main.go` File

Create a `main.go` file to use the DHCP client functionality.

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
        fmt.Println("Usage: dhcpclient <network_interface>")
        os.Exit(1)
    }

    iface := os.Args[1]
    packet, err := RequestIP(iface)
    if err != nil {
        log.Fatalf("Failed to request IP: %v", err)
    }

    fmt.Printf("Received DHCP offer: %v\n", packet.YourIPAddr)
}
```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go <network_interface>
```

Replace `<network_interface>` with the name of the network interface you want to use (e.g., `eth0` on Linux or `en0` on macOS). This will request an IP address from a DHCP server and print the received IP address.