# SSH Client

To create an SSH client program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `client.go` file for the client functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir sshclient
cd sshclient
go mod init github.com/username/sshclient
```

## Step 2: Create the `client.go` File

Create a `client.go` file to handle the SSH client functionality.

```go
// client.go
package main

import (
    "golang.org/x/crypto/ssh"
    "io/ioutil"
    "log"
    "os"
)

// SSHClient represents an SSH client.
type SSHClient struct {
    client *ssh.Client
}

// NewSSHClient creates a new SSH client.
func NewSSHClient(user, password, host string, port int) (*SSHClient, error) {
    config := &ssh.ClientConfig{
        User: user,
        Auth: []ssh.AuthMethod{
            ssh.Password(password),
        },
        HostKeyCallback: ssh.InsecureIgnoreHostKey(),
    }

    address := fmt.Sprintf("%s:%d", host, port)
    client, err := ssh.Dial("tcp", address, config)
    if err != nil {
        return nil, err
    }

    return &SSHClient{client: client}, nil
}

// RunCommand runs a command on the remote SSH server.
func (s *SSHClient) RunCommand(cmd string) (string, error) {
    session, err := s.client.NewSession()
    if err != nil {
        return "", err
    }
    defer session.Close()

    output, err := session.CombinedOutput(cmd)
    if err != nil {
        return "", err
    }

    return string(output), nil
}

// Close closes the SSH client connection.
func (s *SSHClient) Close() error {
    return s.client.Close()
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
    "strconv"
)

func main() {
    if len(os.Args) != 6 {
        fmt.Println("Usage: sshclient <user> <password> <host> <port> <command>")
        os.Exit(1)
    }

    user := os.Args[1]
    password := os.Args[2]
    host := os.Args[3]
    port, err := strconv.Atoi(os.Args[4])
    if err != nil {
        fmt.Printf("Invalid port: %v\n", err)
        os.Exit(1)
    }
    command := os.Args[5]

    client, err := NewSSHClient(user, password, host, port)
    if err != nil {
        fmt.Printf("Failed to create SSH client: %v\n", err)
        os.Exit(1)
    }
    defer client.Close()

    output, err := client.RunCommand(command)
    if err != nil {
        fmt.Printf("Failed to run command: %v\n", err)
        os.Exit(1)
    }

    fmt.Println("Command output:", output)
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go username password host 22 "ls -l"
```

This will connect to the SSH server at the specified host and port, run the given command, and print the output.