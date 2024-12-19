# FTPS Client

To create an FTPS client program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `client.go` file for the client functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir ftpsclient
cd ftpsclient
go mod init github.com/username/ftpsclient
```

## Step 2: Create the `client.go` File

Create a `client.go` file to handle the FTPS client functionality.

```go
// client.go
package main

import (
    "crypto/tls"
    "fmt"
    "github.com/jlaffaye/ftp"
    "io/ioutil"
)

// FetchFile fetches the content of the specified file from the FTPS server.
func FetchFile(server, user, password, filePath string) (string, error) {
    // Configure TLS settings
    tlsConfig := &tls.Config{
        InsecureSkipVerify: true, // Skip certificate verification for simplicity
    }

    // Connect to the FTPS server
    conn, err := ftp.Dial(server, ftp.DialWithTLS(tlsConfig))
    if err != nil {
        return "", err
    }
    defer conn.Quit()

    // Login to the server
    if err := conn.Login(user, password); err != nil {
        return "", err
    }

    // Retrieve the file
    resp, err := conn.Retr(filePath)
    if err != nil {
        return "", err
    }
    defer resp.Close()

    // Read the file content
    body, err := ioutil.ReadAll(resp)
    if err != nil {
        return "", err
    }

    return string(body), nil
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
    if len(os.Args) != 5 {
        fmt.Println("Usage: ftpsclient <server> <user> <password> <filePath>")
        os.Exit(1)
    }

    server := os.Args[1]
    user := os.Args[2]
    password := os.Args[3]
    filePath := os.Args[4]

    content, err := FetchFile(server, user, password, filePath)
    if err != nil {
        fmt.Printf("Failed to fetch file %s: %v\n", filePath, err)
        os.Exit(1)
    }

    fmt.Printf("Content of %s:\n%s\n", filePath, content)
}
```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go ftps.example.com username password /path/to/file.txt
```

This will fetch and print the content of the specified file from the FTPS server.