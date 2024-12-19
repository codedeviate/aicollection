# Firewall

To create a firewall program in Go, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir firewall
cd firewall
go mod init github.com/username/firewall
```

## Step 2: Install Dependencies

You will need the `gopacket` library for packet handling.

```sh
go get github.com/google/gopacket
```

## Step 3: Create the `firewall.go` File

Create a `firewall.go` file to handle the firewall functionality.

```go
// firewall.go
package main

import (
    "fmt"
    "github.com/google/gopacket"
    "github.com/google/gopacket/layers"
    "github.com/google/gopacket/pcap"
    "log"
    "net"
)

// Rule represents a firewall rule.
type Rule struct {
    SrcIP   net.IP
    DstIP   net.IP
    SrcPort layers.TCPPort
    DstPort layers.TCPPort
    Action  string // "allow" or "deny"
}

// Firewall represents a simple firewall.
type Firewall struct {
    rules []Rule
}

// NewFirewall creates a new Firewall.
func NewFirewall() *Firewall {
    return &Firewall{}
}

// AddRule adds a rule to the firewall.
func (fw *Firewall) AddRule(rule Rule) {
    fw.rules = append(fw.rules, rule)
}

// CheckPacket checks if a packet matches any rule.
func (fw *Firewall) CheckPacket(packet gopacket.Packet) bool {
    ipLayer := packet.Layer(layers.LayerTypeIPv4)
    tcpLayer := packet.Layer(layers.LayerTypeTCP)

    if ipLayer != nil && tcpLayer != nil {
        ip, _ := ipLayer.(*layers.IPv4)
        tcp, _ := tcpLayer.(*layers.TCP)

        for _, rule := range fw.rules {
            if rule.SrcIP.Equal(ip.SrcIP) && rule.DstIP.Equal(ip.DstIP) &&
                rule.SrcPort == tcp.SrcPort && rule.DstPort == tcp.DstPort {
                return rule.Action == "allow"
            }
        }
    }
    return false
}

// StartFirewall starts the firewall on the specified interface.
func StartFirewall(iface string, fw *Firewall) {
    handle, err := pcap.OpenLive(iface, 1600, true, pcap.BlockForever)
    if err != nil {
        log.Fatalf("Failed to open device: %v", err)
    }
    defer handle.Close()

    packetSource := gopacket.NewPacketSource(handle, handle.LinkType())
    for packet := range packetSource.Packets() {
        if fw.CheckPacket(packet) {
            fmt.Println("Packet allowed")
        } else {
            fmt.Println("Packet denied")
        }
    }
}
```

## Step 4: Create the `main.go` File

Create a `main.go` file to use the firewall functionality.

```go
// main.go
package main

import (
    "fmt"
    "net"
    "os"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: firewall <network_interface>")
        os.Exit(1)
    }

    iface := os.Args[1]

    fw := NewFirewall()
    fw.AddRule(Rule{
        SrcIP:   net.IPv4(192, 168, 1, 1),
        DstIP:   net.IPv4(192, 168, 1, 2),
        SrcPort: 80,
        DstPort: 80,
        Action:  "allow",
    })

    fmt.Printf("Starting firewall on interface %s...\n", iface)
    StartFirewall(iface, fw)
}
```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go <network_interface>
```

Replace `<network_interface>` with the name of the network interface you want to use (e.g., `eth0` on Linux or `en0` on macOS). This will start the firewall on the specified network interface.