# FTP Server

To create an FTP server program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `server.go` file for the server functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir ftpserver
cd ftpserver
go mod init github.com/username/ftpserver
```

## Step 2: Create the `server.go` File

Create a `server.go` file to handle the FTP server functionality.

```go
// server.go
package main

import (
    "log"
    "github.com/goftp/server"
)

// StartServer starts the FTP server on the specified port.
func StartServer(port string) error {
    factory := &server.SimplePerm{
        User: "test",
        Pass: "1234",
    }

    driver, err := server.NewFileDriver("/tmp")
    if err != nil {
        return err
    }

    opts := &server.ServerOpts{
        Factory:  factory,
        Port:     port,
        Driver:   driver,
        Auth:     &server.SimpleAuth{Name: "test", Password: "1234"},
        Perm:     factory,
    }

    ftpServer := server.NewServer(opts)
    return ftpServer.ListenAndServe()
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
        fmt.Println("Usage: ftpserver <port>")
        os.Exit(1)
    }

    port := os.Args[1]
    fmt.Printf("Starting FTP server on port %s...\n", port)
    if err := StartServer(port); err != nil {
        fmt.Printf("Server failed: %v\n", err)
        os.Exit(1)
    }
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go 2121
```

This will start the FTP server on port 2121. You can connect to it using an FTP client with the username `test` and password `1234`.