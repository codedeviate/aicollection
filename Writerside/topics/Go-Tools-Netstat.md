# Netstat

To implement the `Netstat` functionality in Go, you can use the `net` package to retrieve the list of active network connections. However, Go's standard library does not provide a direct way to list all active connections. Instead, you can use the `netstat` command available on Unix-like systems and parse its output.

Here is an example implementation:

## Step 2: Update the `netstat.go` File

Create a `netstatmod/netstat.go` file to handle the `Netstat` functionality.

```go
// netstat.go
package netstat

import (
	"bufio"
	"os/exec"
	"strings"
)

// Netstat retrieves the list of active network connections.
func Netstat() ([]string, error) {
    cmd := exec.Command("netstat", "-an")
    stdout, err := cmd.Output()
    if err != nil {
        return nil, err
    }

    scanner := bufio.NewScanner(strings.NewReader(string(stdout)))
    var connections []string
    for scanner.Scan() {
        connections = append(connections, scanner.Text())
    }
    if err := scanner.Err(); err != nil {
        return nil, err
    }
    return connections, nil
}

```

## Step 3: Update the `main.go` File

Create a `main.go` file to use the `Netstat` functionality.

```go
// main.go
package main

import (
	"fmt"
	"os"

	netstat "github.com/username/netstat/netstatmod"
)

func main() {
	connections, err := netstat.Netstat()
	if err != nil {
		fmt.Printf("Netstat failed: %v\n", err)
		os.Exit(1)
	}

	fmt.Println("Active network connections:")
	for _, conn := range connections {
		fmt.Println(conn)
	}
}

```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go
```

This will output the active network connections by executing the `netstat -an` command and parsing its output.