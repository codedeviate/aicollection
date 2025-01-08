# Subsystem

To create a program in Go that scans for subsystems (e.g., PHP, Python, or other technologies running on a web server), you need to create a few files: `main.go` for the main logic, and optionally, a `server.go` file for the scanning functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir subsystem
cd subsystem
mkdir lib
go mod init github.com/username/subsystem
```

## Step 2: Create the `subsystem.go` File

Create a `lib/server.go` file to handle the functionality of identifying subsystems.

```go
package lib

import (
	"fmt"
	"net/http"
	"strings"
)

// GetServerInfo fetches the headers of the given URL and tries to identify the server and its version.
func GetServerInfo(url string) {
	// Ensure the URL starts with http:// or https://
	if !strings.HasPrefix(url, "http://") && !strings.HasPrefix(url, "https://") {
		url = "http://" + url
	}

	resp, err := http.Get(url)
	if err != nil {
		fmt.Printf("Error fetching URL %s: %v\n", url, err)
		return
	}
	defer resp.Body.Close()

	fmt.Printf("Headers for %s:\n", url)
	for key, values := range resp.Header {
		for _, value := range values {
			fmt.Printf("%s: %s\n", key, value)
		}
	}

	// Try to extract specific information
	server := resp.Header.Get("Server")
	if server != "" {
		fmt.Printf("\nDetected Server: %s\n", server)
	} else {
		fmt.Println("\nServer information not found in headers.")
	}

	xPoweredBy := resp.Header.Get("X-Powered-By")
	if xPoweredBy != "" {
		fmt.Printf("Detected Subsystem (e.g., PHP, Python): %s\n", xPoweredBy)
	} else {
		fmt.Println("Subsystem information not found in headers.")
	}
}

```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the subsystem scanning functionality.

```go
package main

import (
	"fmt"
	"os"

	"github.com/username/subsystem/lib"
)

func main() {
	var url string

	if len(os.Args) > 1 {
		url = os.Args[1]
	} else {
		fmt.Print("Enter the URL (e.g., example.com): ")
		fmt.Scanln(&url)
	}

	lib.GetServerInfo(url)
}

```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go example.com
```

The program will fetch the headers from the specified URL and attempt to detect:
1. The subsystem (e.g., PHP, Python) using the `X-Powered-By` header.
2. The web server software using the `Server` header.

### Example Output

For a server running Apache with PHP:
```
Headers for http://example.com:
Server: Apache/2.4.41 (Ubuntu)
X-Powered-By: PHP/7.4.3
...

Detected Server: Apache/2.4.41 (Ubuntu)
Detected Subsystem (e.g., PHP, Python): PHP/7.4.3
```

### Notes
- This program relies on the headers provided by the server. If the server suppresses or obfuscates headers for security reasons, detection may be limited.
- The program can be extended to include fingerprinting techniques for more detailed subsystem identification.