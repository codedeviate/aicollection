# DNS Server

To create a DNS server program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `dnsserver.go` file for the DNS server functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir dnsserver
cd dnsserver
go mod init github.com/username/dnsserver
```

## Step 2: Install Dependencies

You will need the `miekg/dns` library for DNS server functionality.

```sh
go get github.com/miekg/dns
```

## Step 3: Create the `dnsserver.go` File

Create a `dnsserver.go` file to handle the DNS server functionality.

```go
// dnsserver.go
package main

import (
    "github.com/miekg/dns"
    "log"
    "net"
)

// handleDNSRequest handles incoming DNS requests.
func handleDNSRequest(w dns.ResponseWriter, r *dns.Msg) {
    msg := dns.Msg{}
    msg.SetReply(r)
    msg.Authoritative = true

    switch r.Opcode {
    case dns.OpcodeQuery:
        for _, q := range r.Question {
            switch q.Qtype {
            case dns.TypeA:
                ip := net.ParseIP("127.0.0.1")
                rr := &dns.A{
                    Hdr: dns.RR_Header{
                        Name:   q.Name,
                        Rrtype: dns.TypeA,
                        Class:  dns.ClassINET,
                        Ttl:    0,
                    },
                    A: ip,
                }
                msg.Answer = append(msg.Answer, rr)
            }
        }
    }

    w.WriteMsg(&msg)
}

// StartDNSServer starts the DNS server on the specified port.
func StartDNSServer(port string) {
    server := &dns.Server{Addr: ":" + port, Net: "udp"}
    dns.HandleFunc(".", handleDNSRequest)
    log.Printf("Starting DNS server on port %s", port)
    err := server.ListenAndServe()
    if err != nil {
        log.Fatalf("Failed to start DNS server: %v", err)
    }
}
```

## Step 4: Create the `main.go` File

Create a `main.go` file to use the DNS server functionality.

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
        fmt.Println("Usage: dnsserver <port>")
        os.Exit(1)
    }

    port := os.Args[1]

    fmt.Printf("Starting DNS server on port %s...\n", port)
    StartDNSServer(port)
}
```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go 53
```

This will start the DNS server on port 53. The server will respond to DNS queries with a fixed IP address (127.0.0.1).