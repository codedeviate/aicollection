# HTTP Server

To create an HTTP server program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `server.go` file for the server functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir httpserver
cd httpserver
go mod init github.com/username/httpserver
```

## Step 2: Create the `server.go` File

Create a `server.go` file to handle the HTTP server functionality.

```go
// server.go
package main

import (
    "fmt"
    "net/http"
)

// handler is a simple HTTP handler function.
func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!")
}

// StartServer starts the HTTP server on the specified port.
func StartServer(port string) error {
    http.HandleFunc("/", handler)
    return http.ListenAndServe(":"+port, nil)
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
        fmt.Println("Usage: httpserver <port>")
        os.Exit(1)
    }

    port := os.Args[1]
    fmt.Printf("Starting server on port %s...\n", port)
    if err := StartServer(port); err != nil {
        fmt.Printf("Server failed: %v\n", err)
        os.Exit(1)
    }
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go 8080
```

This will start the HTTP server on port 8080. You can access it by navigating to `http://localhost:8080` in your web browser.