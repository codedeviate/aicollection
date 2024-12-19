# SMTP Client

To create an SMTP client program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `client.go` file for the client functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir smtpclient
cd smtpclient
go mod init github.com/username/smtpclient
```

## Step 2: Create the `client.go` File

Create a `client.go` file to handle the SMTP client functionality.

```go
// client.go
package main

import (
    "crypto/tls"
    "fmt"
    "log"
    "net/smtp"
)

// SendEmail sends an email using the specified SMTP server.
func SendEmail(server, port, user, password, from, to, subject, body string) error {
    auth := smtp.PlainAuth("", user, password, server)

    msg := []byte("To: " + to + "\r\n" +
        "Subject: " + subject + "\r\n" +
        "\r\n" + body + "\r\n")

    addr := server + ":" + port
    tlsconfig := &tls.Config{
        InsecureSkipVerify: true,
        ServerName:         server,
    }

    conn, err := tls.Dial("tcp", addr, tlsconfig)
    if err != nil {
        return err
    }
    defer conn.Close()

    c, err := smtp.NewClient(conn, server)
    if err != nil {
        return err
    }
    defer c.Quit()

    if err = c.Auth(auth); err != nil {
        return err
    }

    if err = c.Mail(from); err != nil {
        return err
    }

    if err = c.Rcpt(to); err != nil {
        return err
    }

    w, err := c.Data()
    if err != nil {
        return err
    }

    _, err = w.Write(msg)
    if err != nil {
        return err
    }

    err = w.Close()
    if err != nil {
        return err
    }

    return c.Quit()
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the client functionality.

```go
// main.go
package main

import (
    "fmt"
    "os"
)

func main() {
    if len(os.Args) != 9 {
        fmt.Println("Usage: smtpclient <server> <port> <user> <password> <from> <to> <subject> <body>")
        os.Exit(1)
    }

    server := os.Args[1]
    port := os.Args[2]
    user := os.Args[3]
    password := os.Args[4]
    from := os.Args[5]
    to := os.Args[6]
    subject := os.Args[7]
    body := os.Args[8]

    err := SendEmail(server, port, user, password, from, to, subject, body)
    if err != nil {
        fmt.Printf("Failed to send email: %v\n", err)
        os.Exit(1)
    }

    fmt.Println("Email sent successfully")
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go smtp.example.com 587 username password from@example.com to@example.com "Subject" "Email body"
```

This will send an email using the specified SMTP server.