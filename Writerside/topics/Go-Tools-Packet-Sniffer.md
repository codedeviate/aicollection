# Packet Sniffer

To create a packet sniffer program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `sniffer.go` file for the sniffer functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir packetsniffer
cd packetsniffer
go mod init github.com/username/packetsniffer
```

## Step 2: Install Dependencies

You will need the `gopacket` library for packet capturing and decoding.

```sh
go get github.com/google/gopacket
go get github.com/google/gopacket/pcap
```

## Step 3: Create the `sniffer.go` File

Create a `sniffer.go` file to handle the packet sniffing functionality.

```go
// sniffer.go
package main

import (
    "fmt"
    "log"
    "github.com/google/gopacket"
    "github.com/google/gopacket/pcap"
    "time"
)

// SniffPackets captures and prints packets from the specified network interface.
func SniffPackets(device string, snapshotLen int32, promiscuous bool, timeout time.Duration) error {
    handle, err := pcap.OpenLive(device, snapshotLen, promiscuous, timeout)
    if err != nil {
        return err
    }
    defer handle.Close()

    packetSource := gopacket.NewPacketSource(handle, handle.LinkType())
    for packet := range packetSource.Packets() {
        fmt.Println(packet)
    }

    return nil
}
```

## Step 4: Create the `main.go` File

Create a `main.go` file to use the sniffer functionality.

```go
// main.go
package main

import (
    "fmt"
    "log"
    "os"
    "time"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: packetsniffer <network_interface>")
        os.Exit(1)
    }

    device := os.Args[1]
    snapshotLen := int32(1024)
    promiscuous := false
    timeout := 30 * time.Second

    fmt.Printf("Starting packet sniffer on interface %s...\n", device)
    if err := SniffPackets(device, snapshotLen, promiscuous, timeout); err != nil {
        log.Fatalf("Error sniffing packets: %v", err)
    }
}
```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go <network_interface>
```

Replace `<network_interface>` with the name of the network interface you want to sniff packets on (e.g., `eth0` on Linux or `en0` on macOS). This will start capturing and printing packets from the specified network interface.