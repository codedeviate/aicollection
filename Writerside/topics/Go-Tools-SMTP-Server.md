# SMTP Server

To create an SMTP server program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `server.go` file for the server functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir smtpserver
cd smtpserver
go mod init github.com/username/smtpserver
```

## Step 2: Create the `server.go` File

Create a `server.go` file to handle the SMTP server functionality.

```go
// server.go
package main

import (
    "log"
    "net"
    "github.com/emersion/go-smtp"
)

// Backend implements SMTP server methods.
type Backend struct{}

// Login handles login for the SMTP server.
func (bkd *Backend) Login(state *smtp.ConnectionState, username, password string) (smtp.Session, error) {
    return &Session{}, nil
}

// AnonymousLogin allows anonymous login.
func (bkd *Backend) AnonymousLogin(state *smtp.ConnectionState) (smtp.Session, error) {
    return &Session{}, nil
}

// A Session is returned after successful login.
type Session struct{}

// Mail handles the MAIL command.
func (s *Session) Mail(from string, opts smtp.MailOptions) error {
    log.Println("Mail from:", from)
    return nil
}

// Rcpt handles the RCPT command.
func (s *Session) Rcpt(to string) error {
    log.Println("Rcpt to:", to)
    return nil
}

// Data handles the DATA command.
func (s *Session) Data(r io.Reader) error {
    log.Println("Data received")
    return nil
}

// Reset handles the RSET command.
func (s *Session) Reset() {}

// Logout handles the LOGOUT command.
func (s *Session) Logout() error {
    return nil
}

// StartServer starts the SMTP server on the specified port.
func StartServer(port string) error {
    be := &Backend{}
    s := smtp.NewServer(be)

    s.Addr = ":" + port
    s.Domain = "localhost"
    s.ReadTimeout = 10 * time.Second
    s.WriteTimeout = 10 * time.Second
    s.MaxMessageBytes = 1024 * 1024
    s.MaxRecipients = 50
    s.AllowInsecureAuth = true

    log.Println("Starting SMTP server on port", port)
    return s.ListenAndServe()
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
        fmt.Println("Usage: smtpserver <port>")
        os.Exit(1)
    }

    port := os.Args[1]
    fmt.Printf("Starting SMTP server on port %s...\n", port)
    if err := StartServer(port); err != nil {
        fmt.Printf("Server failed: %v\n", err)
        os.Exit(1)
    }
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go 2525
```

This will start the SMTP server on port 2525. You can connect to it using an SMTP client.