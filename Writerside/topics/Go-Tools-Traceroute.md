# Traceroute

To create a traceroute program in Go, you need to create a few files: `main.go` for the main logic, and optionally, a `traceroute.go` file for the traceroute functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir traceroute
cd traceroute
mkdir traceroutemod
go mod init github.com/username/traceroute
```

## Step 2: Create the `traceroute.go` File

Create a `traceroute.go` file in the `traceroutemod` directory to handle the traceroute functionality.

```go
package traceroute

import (
	"fmt"
	"net"
	"strings"
	"time"

	"golang.org/x/net/icmp"
	"golang.org/x/net/ipv4"
)

// Config struct holds configuration values for the traceroute operation
// including whether to resolve DNS names and the maximum number of hops and timeout.
// The struct also includes flags to skip hops 1-5 which normally can cause timeouts.
type Config struct {
	Dns      *bool    // DNS resolution flag for hop addresses
	Hops     *int     // Maximum number of hops
	Timeout  *float64 // Timeout in seconds for each hop
	SkipHop1 *bool    // Skip hop 1
	SkipHop2 *bool    // Skip hop 2
	SkipHop3 *bool    // Skip hop 3
	SkipHop4 *bool    // Skip hop 4
	SkipHop5 *bool    // Skip hop 5
}

// Traceroute performs a traceroute to the specified address.
// It sends ICMP Echo requests to the target IP and prints the route
// taken by the packets, showing the response times for each hop.
func Traceroute(address string, config Config) error {
	// Resolve the target address to an IP address
	targetAddr, err := net.ResolveIPAddr("ip4", address)
	if err != nil {
		return fmt.Errorf("failed to resolve address: %v", err)
	}

	// Loop over the TTL values to simulate the hop count
	for ttl := 1; ttl <= *config.Hops; ttl++ {
		if ttl == 1 && *config.SkipHop1 {
			fmt.Println("Hop 1: Skipped")
			continue
		} else if ttl == 2 && *config.SkipHop2 {
			fmt.Println("Hop 2: Skipped")
			continue
		} else if ttl == 3 && *config.SkipHop3 {
			fmt.Println("Hop 3: Skipped")
			continue
		} else if ttl == 4 && *config.SkipHop4 {
			fmt.Println("Hop 4: Skipped")
			continue
		} else if ttl == 5 && *config.SkipHop5 {
			fmt.Println("Hop 5: Skipped")
			continue
		}

		// Listen for ICMP packets on the network
		conn, err := icmp.ListenPacket("ip4:icmp", "0.0.0.0")
		if err != nil {
			return fmt.Errorf("failed to create connection: %v", err)
		}
		defer conn.Close() // Ensure the connection is closed when done

		// Create an IPv4 packet connection for sending and receiving
		ipv4conn := conn.IPv4PacketConn()
		defer ipv4conn.Close() // Ensure IPv4 packet connection is closed when done

		// Set the TTL value for the outgoing packet
		if err := ipv4conn.SetTTL(ttl); err != nil {
			return fmt.Errorf("failed to set TTL: %v", err)
		}
		ipv4conn.SetControlMessage(ipv4.FlagTTL, true) // Enable TTL information in the control message

		// Create the ICMP Echo Request message
		message := []byte("traceroute") // Data for the ICMP packet
		icmpMessage := icmp.Message{
			Type: ipv4.ICMPTypeEcho, // Set the message type as Echo Request
			Code: 0,
			Body: &icmp.Echo{
				ID:   ttl, // Use TTL as ID to simplify tracking
				Seq:  1,
				Data: message,
			},
		}

		// Marshal the ICMP message into a byte slice
		icmpBytes, err := icmpMessage.Marshal(nil)
		if err != nil {
			return fmt.Errorf("failed to marshal ICMP message: %v", err)
		}

		// Record the time before sending the request
		start := time.Now()

		// Send the ICMP message to the target IP address
		if _, err := ipv4conn.WriteTo(icmpBytes, nil, &net.UDPAddr{IP: targetAddr.IP}); err != nil {
			return fmt.Errorf("failed to send ICMP message: %v", err)
		}

		// Wait for a reply from the target
		buffer := make([]byte, 1500)

		// Set the timeout duration in milliseconds and apply it to the connection read deadline
		timeout := int(*config.Timeout*1000) * int(time.Millisecond)
		err = conn.SetReadDeadline(time.Now().Add(time.Duration(timeout)))

		if err != nil {
			return fmt.Errorf("failed to set read deadline: %v", err)
		}

		// Read the reply from the target (or timeout if no response)
		n, cm, _, err := ipv4conn.ReadFrom(buffer)
		if err != nil {
			// If no response within the timeout, print a timeout message
			fmt.Printf("Hop %d: Request timed out\n", ttl)
			continue
		}

		// Calculate the round-trip duration
		duration := time.Since(start)

		// Parse the received ICMP Echo Reply message
		_, err = icmp.ParseMessage(ipv4.ICMPTypeEchoReply.Protocol(), buffer[:n])
		if err != nil {
			return fmt.Errorf("failed to parse ICMP reply: %v", err)
		}

		// Extract the source address and return TTL from the control message
		remoteAddress := "?.?.?.?" // Default value if no control message
		returnTTL := -1
		if cm != nil {
			remoteAddress = cm.Src.String() // Source IP address of the reply
			returnTTL = cm.TTL              // TTL returned by the source
		}
		orgRemoteAddress := remoteAddress // Store the original remote address

		// Optionally resolve the DNS name for the remote address if the flag is set
		if *config.Dns {
			names, err := net.LookupAddr(remoteAddress)
			if err == nil && len(names) > 0 {
				remoteAddress = fmt.Sprintf("%s (%s)", strings.Trim(names[0], " ."), remoteAddress)
			}
		}

		// Print the hop information, including the remote address and round-trip time
		fmt.Printf("Hop %d: %v in %v (Return TTL: %d)\n", ttl, remoteAddress, duration, returnTTL)

		// Close the connection before the next iteration
		// By closing the connection, we ensure that the next iteration will use a new socket
		// and the time to close the connection isn't postponed until the end of the function
		// which could cause a delay before the function returns. By using a go routine, we can
		// close the connection asynchronously while the next iteration is running.
		go ipv4conn.Close()

		// If the response address matches the target, we have reached the destination
		if orgRemoteAddress == targetAddr.String() {
			break // Reached destination
		}
	}

	return nil
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the traceroute functionality.

```go
// main.go
package main

import (
	"flag" // Import the flag package to handle command-line arguments
	"fmt"  // Import fmt for formatted I/O
	"os"   // Import os to handle exit codes and file operations

	// Import the traceroute package that contains the actual traceroute logic
	traceroute "github.com/username/traceroute/traceroutemod"
)

func main() {
	// Define and parse command-line flags:
	// - `-d` for DNS lookup (whether to resolve hostnames)
	// - `-h` for maximum number of hops (default is 30)
	// - `-t` for timeout in seconds (default is 3 seconds)
	config := traceroute.Config{
		Dns:      flag.Bool("d", false, "Do DNS lookup"),     // Boolean flag for DNS lookup
		Hops:     flag.Int("h", 30, "Max hops"),              // Integer flag for max hops
		Timeout:  flag.Float64("t", 3, "Timeout in seconds"), // Float flag for timeout duration in seconds
		SkipHop1: flag.Bool("s1", false, "Skip hop 1"),       // Boolean flag to skip hop 1
		SkipHop2: flag.Bool("s2", false, "Skip hop 2"),       // Boolean flag to skip hop 2
		SkipHop3: flag.Bool("s3", false, "Skip hop 3"),       // Boolean flag to skip hop 3
		SkipHop4: flag.Bool("s4", false, "Skip hop 4"),       // Boolean flag to skip hop 4
		SkipHop5: flag.Bool("s5", false, "Skip hop 5"),       // Boolean flag to skip hop 5
	}

	// Parse the flags to read values from the command-line arguments
	flag.Parse()

	// Ensure there is exactly one positional argument (the target address)
	if len(flag.Args()) != 1 {
		// If not, display the usage and exit with an error code
		flag.Usage()
		os.Exit(1)
	}

	// The first positional argument is the target address for traceroute
	address := flag.Args()[0]

	// Print the starting message for the traceroute
	fmt.Printf("Traceroute to %s:\n", address)

	// Call the Traceroute function from the traceroute package
	// Pass the target address and the configuration values
	err := traceroute.Traceroute(address, config)

	// If there is an error during the traceroute, print the error message and exit
	if err != nil {
		fmt.Printf("Traceroute to %s failed: %v\n", address, err)
		os.Exit(1)
	}
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go example.com
```

This will output the traceroute hops to the specified address.