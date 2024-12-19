# What we have done so far

To combine the functionalities of ping, whois, dig/nslookup, and netscan into one Go program:

1. `main.go` - The main entry point of the program.
2. `ping.go` - Contains the ping functionality.
3. `whois.go` - Contains the whois functionality.
4. `dnslookup.go` - Contains the DNS lookup functionality.
5. `netscan.go` - Contains the network scan functionality.
6. `main_test.go` - Contains the tests for the functionalities.

Here is the implementation:

### `main.go`
```go
package main

import (
    "fmt"
    "os"
    "strconv"
)

func main() {
    if len(os.Args) < 3 {
        fmt.Println("Usage: tool <command> <args>")
        fmt.Println("Commands: ping <host>, whois <domain>, dig <domain>, netscan <hostname> <startPort> <endPort>")
        os.Exit(1)
    }

    command := os.Args[1]
    switch command {
    case "ping":
        if len(os.Args) != 3 {
            fmt.Println("Usage: tool ping <host>")
            os.Exit(1)
        }
        host := os.Args[2]
        if err := Ping(host); err != nil {
            fmt.Printf("Ping failed: %v\n", err)
            os.Exit(1)
        }
    case "whois":
        if len(os.Args) != 3 {
            fmt.Println("Usage: tool whois <domain>")
            os.Exit(1)
        }
        domain := os.Args[2]
        if err := Whois(domain); err != nil {
            fmt.Printf("Whois failed: %v\n", err)
            os.Exit(1)
        }
    case "dig":
        if len(os.Args) != 3 {
            fmt.Println("Usage: tool dig <domain>")
            os.Exit(1)
        }
        domain := os.Args[2]
        ips, err := DNSLookup(domain)
        if err != nil {
            fmt.Printf("DNS lookup for %s failed: %v\n", domain, err)
            os.Exit(1)
        }
        fmt.Printf("DNS lookup result for %s:\n", domain)
        for _, ip := range ips {
            fmt.Println(ip)
        }
    case "netscan":
        if len(os.Args) != 5 {
            fmt.Println("Usage: tool netscan <hostname> <startPort> <endPort>")
            os.Exit(1)
        }
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
        ScanHost(hostname, startPort, endPort)
    default:
        fmt.Println("Unknown command:", command)
        os.Exit(1)
    }
}
```

### `ping.go`
```go
package main

import (
    "os"
    "os/exec"
)

// Ping checks if a host is reachable by sending ICMP echo requests.
func Ping(host string) error {
    cmd := exec.Command("ping", "-c", "4", host)
    cmd.Stdout = os.Stdout
    cmd.Stderr = os.Stderr
    return cmd.Run()
}
```

### `whois.go`
```go
package main

import (
    "os"
    "os/exec"
)

// Whois performs a WHOIS lookup for the given domain.
func Whois(domain string) error {
    cmd := exec.Command("whois", domain)
    cmd.Stdout = os.Stdout
    cmd.Stderr = os.Stderr
    return cmd.Run()
}
```

### `dnslookup.go`
```go
package main

import (
    "fmt"
    "net"
)

// DNSLookup performs a DNS lookup for the given domain and returns the IP addresses.
func DNSLookup(domain string) ([]string, error) {
    ips, err := net.LookupIP(domain)
    if err != nil {
        return nil, err
    }
    var result []string
    for _, ip := range ips {
        result = append(result, ip.String())
    }
    return result, nil
}
```

### `netscan.go`
```go
package main

import (
    "fmt"
    "net"
    "time"
)

// ScanPort checks if a port is open on a given host.
func ScanPort(protocol, hostname string, port int) bool {
    address := fmt.Sprintf("%s:%d", hostname, port)
    conn, err := net.DialTimeout(protocol, address, time.Second)
    if err != nil {
        return false
    }
    conn.Close()
    return true
}

// ScanHost scans a range of ports on a given host.
func ScanHost(hostname string, startPort, endPort int) {
    for port := startPort; port <= endPort; port++ {
        if ScanPort("tcp", hostname, port) {
            fmt.Printf("Port %d is open\n", port)
        }
    }
}
```

### `main_test.go`
```go
package main

import (
    "testing"
)

func TestDNSLookup(t *testing.T) {
    domain := "example.com"
    ips, err := DNSLookup(domain)
    if err != nil {
        t.Fatalf("DNSLookup failed: %v", err)
    }
    if len(ips) == 0 {
        t.Fatalf("DNSLookup returned no IPs for %s", domain)
    }
}

func TestScanPort(t *testing.T) {
    hostname := "localhost"
    port := 80
    if !ScanPort("tcp", hostname, port) {
        t.Fatalf("Port %d on %s is not open", port, hostname)
    }
}
```

This setup splits the functionalities into separate files and adds basic tests for DNS lookup and port scanning. You can run the tests using the `go test` command.