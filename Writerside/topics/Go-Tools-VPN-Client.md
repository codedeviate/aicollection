# VPN Client

To create a VPN client program in Go, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir vpnclient
cd vpnclient
go mod init github.com/username/vpnclient
```

## Step 2: Install Dependencies

You will need the `gopacket` library for packet handling and `tun2socks` for tunneling.

```sh
go get github.com/google/gopacket
go get github.com/eycorsican/go-tun2socks
```

## Step 3: Create the `vpnclient.go` File

Create a `vpnclient.go` file to handle the VPN client functionality.

```go
// vpnclient.go
package main

import (
    "fmt"
    "github.com/eycorsican/go-tun2socks/core"
    "github.com/google/gopacket"
    "github.com/google/gopacket/layers"
    "github.com/google/gopacket/pcap"
    "log"
    "os"
    "os/signal"
    "syscall"
)

// StartVPNClient starts the VPN client.
func StartVPNClient(iface string) {
    handle, err := pcap.OpenLive(iface, 1600, true, pcap.BlockForever)
    if err != nil {
        log.Fatalf("Failed to open device: %v", err)
    }
    defer handle.Close()

    packetSource := gopacket.NewPacketSource(handle, handle.LinkType())
    for packet := range packetSource.Packets() {
        processPacket(packet)
    }
}

// processPacket processes a single packet.
func processPacket(packet gopacket.Packet) {
    ipLayer := packet.Layer(layers.LayerTypeIPv4)
    if ipLayer != nil {
        ip, _ := ipLayer.(*layers.IPv4)
        fmt.Printf("From %s to %s\n", ip.SrcIP, ip.DstIP)
    }
}
```

## Step 4: Create the `main.go` File

Create a `main.go` file to use the VPN client functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
    "os/signal"
    "syscall"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: vpnclient <network_interface>")
        os.Exit(1)
    }

    iface := os.Args[1]

    go StartVPNClient(iface)

    // Handle termination signals
    sigs := make(chan os.Signal, 1)
    signal.Notify(sigs, syscall.SIGINT, syscall.SIGTERM)
    <-sigs

    fmt.Println("Shutting down VPN client...")
}
```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go <network_interface>
```

Replace `<network_interface>` with the name of the network interface you want to use (e.g., `eth0` on Linux or `en0` on macOS). This will start the VPN client on the specified network interface.