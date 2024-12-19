# SSH Server

To create an SSH server program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `server.go` file for the server functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir sshserver
cd sshserver
go mod init github.com/username/sshserver
```

## Step 2: Create the `server.go` File

Create a `server.go` file to handle the SSH server functionality.

```go
// server.go
package main

import (
    "io"
    "log"
    "net"
    "os"

    "golang.org/x/crypto/ssh"
)

// handleConnection handles incoming SSH connections.
func handleConnection(conn net.Conn, config *ssh.ServerConfig) {
    sshConn, chans, reqs, err := ssh.NewServerConn(conn, config)
    if err != nil {
        log.Printf("Failed to handshake: %v", err)
        return
    }
    defer sshConn.Close()

    go ssh.DiscardRequests(reqs)

    for newChannel := range chans {
        if newChannel.ChannelType() != "session" {
            newChannel.Reject(ssh.UnknownChannelType, "unknown channel type")
            continue
        }

        channel, requests, err := newChannel.Accept()
        if err != nil {
            log.Printf("Could not accept channel: %v", err)
            return
        }

        go func(in <-chan *ssh.Request) {
            for req := range in {
                switch req.Type {
                case "shell":
                    if len(req.Payload) == 0 {
                        req.Reply(true, nil)
                    }
                }
            }
        }(requests)

        go func() {
            io.Copy(channel, channel)
            channel.Close()
        }()
    }
}

// StartServer starts the SSH server on the specified port.
func StartServer(port string, config *ssh.ServerConfig) error {
    listener, err := net.Listen("tcp", ":"+port)
    if err != nil {
        return err
    }
    defer listener.Close()

    log.Printf("SSH server started on port %s", port)
    for {
        conn, err := listener.Accept()
        if err != nil {
            return err
        }
        go handleConnection(conn, config)
    }
}
```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the server functionality.

```go
// main.go
package main

import (
    "fmt"
    "io/ioutil"
    "log"
    "os"

    "golang.org/x/crypto/ssh"
)

func main() {
    if len(os.Args) != 3 {
        fmt.Println("Usage: sshserver <port> <private_key_file>")
        os.Exit(1)
    }

    port := os.Args[1]
    privateKeyFile := os.Args[2]

    privateBytes, err := ioutil.ReadFile(privateKeyFile)
    if err != nil {
        log.Fatalf("Failed to load private key: %v", err)
    }

    private, err := ssh.ParsePrivateKey(privateBytes)
    if err != nil {
        log.Fatalf("Failed to parse private key: %v", err)
    }

    config := &ssh.ServerConfig{
        NoClientAuth: true,
    }
    config.AddHostKey(private)

    fmt.Printf("Starting SSH server on port %s...\n", port)
    if err := StartServer(port, config); err != nil {
        log.Fatalf("Server failed: %v", err)
    }
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go 2222 path/to/private_key
```

This will start the SSH server on port 2222. You can connect to it using an SSH client.