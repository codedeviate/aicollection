# Reverse Proxy

To create a reverse proxy program in Go, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir reverseproxy
cd reverseproxy
go mod init github.com/username/reverseproxy
```

## Step 2: Install Dependencies

You will need the `gorilla/mux` library for routing.

```sh
go get github.com/gorilla/mux
```

## Step 3: Create the `reverseproxy.go` File

Create a `reverseproxy.go` file to handle the reverse proxy functionality.

```go
// reverseproxy.go
package main

import (
    "log"
    "net/http"
    "net/http/httputil"
    "net/url"
    "github.com/gorilla/mux"
)

type Proxy struct {
    target *url.URL
    proxy  *httputil.ReverseProxy
}

func NewProxy(target string) *Proxy {
    url, _ := url.Parse(target)
    return &Proxy{target: url, proxy: httputil.NewSingleHostReverseProxy(url)}
}

func (p *Proxy) handle(w http.ResponseWriter, r *http.Request) {
    r.URL.Host = p.target.Host
    r.URL.Scheme = p.target.Scheme
    r.Header.Set("X-Forwarded-Host", r.Header.Get("Host"))
    r.Host = p.target.Host
    p.proxy.ServeHTTP(w, r)
}

func main() {
    target := "http://localhost:8081" // Target server
    proxy := NewProxy(target)

    r := mux.NewRouter()
    r.PathPrefix("/").HandlerFunc(proxy.handle)

    log.Println("Starting reverse proxy on :8080")
    log.Fatal(http.ListenAndServe(":8080", r))
}
```

## Step 4: Create the `main.go` File

Create a `main.go` file to start the reverse proxy.

```go
// main.go
package main

func main() {
    main()
}
```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go
```

This will start the reverse proxy on port 8080, forwarding requests to the target server specified in the `target` variable.