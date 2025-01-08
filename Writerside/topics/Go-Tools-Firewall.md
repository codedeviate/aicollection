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

Create a `lib/firewall.go` file to handle the firewall functionality.

```go
// firewall.go
package lib

import (
	"fmt"
	"log"
	"net"
	"time"

	"github.com/google/gopacket"
	"github.com/google/gopacket/layers"
	"github.com/google/gopacket/pcap"
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
			fmt.Printf("[%s] Packet allowed: From %s, To: %s\n", time.Now().UTC(), packet.NetworkLayer().NetworkFlow().Src().String(), packet.NetworkLayer().NetworkFlow().Dst().String())
		} else {
			fmt.Printf("[%s] Packet denied: From %s, To: %s\n", time.Now().UTC(), packet.NetworkLayer().NetworkFlow().Src().String(), packet.NetworkLayer().NetworkFlow().Dst().String())
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
	"log"
	"net"
	"os"

	"github.com/username/firewall/lib"
)

func main() {
	if len(os.Args) != 2 {
		fmt.Println("Usage: firewall <network_interface>")
		os.Exit(1)
	}

	iface := os.Args[1]

	physicalIface, err := net.InterfaceByName(iface)
	if err != nil {
		log.Fatalf("could not find interface %s: %v", iface, err)
	}

	addrs, err := physicalIface.Addrs()
	if err != nil {
		log.Fatalf("could not get addresses for interface %s: %v", iface, err)
	}

	fw := lib.NewFirewall()

	for _, addr := range addrs {
		// Check if the address is an IP address
		var ip net.IP
		switch v := addr.(type) {
		case *net.IPNet:
			ip = v.IP
		case *net.IPAddr:
			ip = v.IP
		}

		// Skip loopback addresses
		if ip == nil || ip.IsLoopback() {
			continue
		}

		fw.AddRule(lib.Rule{
			SrcIP:   ip,
			DstIP:   net.IPv4(8, 8, 8, 8),
			SrcPort: 53,
			DstPort: 53,
			Action:  "allow",
		})
	}

	fmt.Printf("Starting firewall on interface %s...\n", iface)
	lib.StartFirewall(iface, fw)
}

```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go <network_interface>
```

Replace `<network_interface>` with the name of the network interface you want to use (e.g., `eth0` on Linux or `en0` on macOS). This will start the firewall on the specified network interface.