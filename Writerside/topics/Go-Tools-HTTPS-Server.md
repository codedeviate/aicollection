# HTTPS Server

To create an HTTPS server program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `server.go` file for the server functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir httpsserver
cd httpsserver
go mod init github.com/username/httpsserver
```

## Step 2: Create the `server.go` File

Create a `server.go` file to handle the HTTPS server functionality.

```go
// server.go
package main

import (
    "fmt"
    "net/http"
)

// handler is a simple HTTP handler function.
func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, HTTPS World!")
}

// StartServer starts the HTTPS server on the specified port.
func StartServer(port, certFile, keyFile string) error {
    http.HandleFunc("/", handler)
    return http.ListenAndServeTLS(":"+port, certFile, keyFile, nil)
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the server functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
)

func main() {
    if len(os.Args) != 4 {
        fmt.Println("Usage: httpsserver <port> <certFile> <keyFile>")
        os.Exit(1)
    }

    port := os.Args[1]
    certFile := os.Args[2]
    keyFile := os.Args[3]
    fmt.Printf("Starting server on port %s...\n", port)
    if err := StartServer(port, certFile, keyFile); err != nil {
        fmt.Printf("Server failed: %v\n", err)
        os.Exit(1)
    }
}
```

## Step 4: Generate SSL Certificates

You need SSL certificates to run the HTTPS server. You can generate self-signed certificates using OpenSSL:

```sh
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go 8080 cert.pem key.pem
```

This will start the HTTPS server on port 8080. You can access it by navigating to `https://localhost:8080` in your web browser.