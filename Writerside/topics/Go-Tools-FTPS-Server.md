# FTPS Server

To create an FTPS server program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `server.go` file for the server functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir ftpsserver
cd ftpsserver
go mod init github.com/username/ftpsserver
```

## Step 2: Create the `server.go` File

Create a `server.go` file to handle the FTPS server functionality.

```go
// server.go
package main

import (
    "crypto/tls"
    "log"
    "github.com/goftp/server"
)

// StartServer starts the FTPS server on the specified port.
func StartServer(port string) error {
    factory := &server.SimplePerm{
        User: "test",
        Pass: "1234",
    }

    driver, err := server.NewFileDriver("/tmp")
    if err != nil {
        return err
    }

    tlsConfig := &tls.Config{
        Certificates: []tls.Certificate{loadCertificate()},
    }

    opts := &server.ServerOpts{
        Factory:  factory,
        Port:     port,
        Driver:   driver,
        Auth:     &server.SimpleAuth{Name: "test", Password: "1234"},
        Perm:     factory,
        TLSConfig: tlsConfig,
    }

    ftpsServer := server.NewServer(opts)
    return ftpsServer.ListenAndServe()
}

func loadCertificate() tls.Certificate {
    cert, err := tls.LoadX509KeyPair("server.crt", "server.key")
    if err != nil {
        log.Fatalf("Failed to load certificate: %v", err)
    }
    return cert
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
    if len(os.Args) != 2 {
        fmt.Println("Usage: ftpsserver <port>")
        os.Exit(1)
    }

    port := os.Args[1]
    fmt.Printf("Starting FTPS server on port %s...\n", port)
    if err := StartServer(port); err != nil {
        fmt.Printf("Server failed: %v\n", err)
        os.Exit(1)
    }
}
```

## Step 4: Generate SSL Certificates

<include from="_openssl.md" element-id="CreateSelfSignedCert"></include>

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go 2121
```

This will start the FTPS server on port 2121. You can connect to it using an FTPS client with the username `test` and password `1234`.