# Bandwidth Monitor

To create a bandwidth monitor program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `monitor.go` file for the bandwidth monitoring functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir bandwidthmonitor
cd bandwidthmonitor
go mod init github.com/username/bandwidthmonitor
```

## Step 2: Install Dependencies

You will need the `gopacket` library for packet capturing and decoding.

```sh
go get github.com/google/gopacket
go get github.com/google/gopacket/pcap
```

## Step 3: Create the `monitor.go` File

Create a `monitor.go` file to handle the bandwidth monitoring functionality.

```go
// monitor.go
package main

import (
    "fmt"
    "github.com/google/gopacket"
    "github.com/google/gopacket/pcap"
    "log"
    "time"
)

type BandwidthMonitor struct {
    device       string
    snapshotLen  int32
    promiscuous  bool
    timeout      time.Duration
    handle       *pcap.Handle
    packetCount  int
    byteCount    int
}

func NewBandwidthMonitor(device string, snapshotLen int32, promiscuous bool, timeout time.Duration) (*BandwidthMonitor, error) {
    handle, err := pcap.OpenLive(device, snapshotLen, promiscuous, timeout)
    if err != nil {
        return nil, err
    }

    return &BandwidthMonitor{
        device:      device,
        snapshotLen: snapshotLen,
        promiscuous: promiscuous,
        timeout:     timeout,
        handle:      handle,
    }, nil
}

func (bm *BandwidthMonitor) Start() {
    packetSource := gopacket.NewPacketSource(bm.handle, bm.handle.LinkType())
    for packet := range packetSource.Packets() {
        bm.packetCount++
        bm.byteCount += len(packet.Data())
    }
}

func (bm *BandwidthMonitor) Stop() {
    bm.handle.Close()
}

func (bm *BandwidthMonitor) Report() {
    fmt.Printf("Packets: %d, Bytes: %d\n", bm.packetCount, bm.byteCount)
}
```

## Step 4: Create the `main.go` File

Create a `main.go` file to use the bandwidth monitoring functionality.

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
        fmt.Println("Usage: bandwidthmonitor <network_interface>")
        os.Exit(1)
    }

    device := os.Args[1]
    snapshotLen := int32(1024)
    promiscuous := false
    timeout := 30 * time.Second

    bm, err := NewBandwidthMonitor(device, snapshotLen, promiscuous, timeout)
    if err != nil {
        log.Fatalf("Error creating bandwidth monitor: %v", err)
    }

    go bm.Start()

    // Monitor for 10 seconds
    time.Sleep(10 * time.Second)

    bm.Stop()
    bm.Report()
}
```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go <network_interface>
```

Replace `<network_interface>` with the name of the network interface you want to monitor (e.g., `eth0` on Linux or `en0` on macOS). This will start monitoring the bandwidth usage on the specified network interface for 10 seconds and then print the report.