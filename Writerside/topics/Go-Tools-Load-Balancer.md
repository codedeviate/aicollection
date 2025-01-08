# Load Balancer

To create a load balancer program in Go, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir loadbalancer
cd loadbalancer
go mod init github.com/username/loadbalancer
```

## Step 2: Install Dependencies

You will need the `gorilla/mux` library for routing.

```sh
go get github.com/gorilla/mux
```

## Step 3: Create the `loadbalancer.go` File

Create a `lib/loadbalancer.go` file to handle the load balancer functionality.

```go
// loadbalancer.go
package lib

import (
	"fmt"
	"log"
	"net/http"
	"net/http/httputil"
	"net/url"
	"sync/atomic"
)

type ServerPool struct {
	servers []*url.URL
	current uint64
}

func (p *ServerPool) AddServer(server *url.URL) {
	p.servers = append(p.servers, server)
}

func (p *ServerPool) NextServer() *url.URL {
	next := atomic.AddUint64(&p.current, uint64(1))
	return p.servers[next%uint64(len(p.servers))]
}

func (p *ServerPool) LoadBalance(w http.ResponseWriter, r *http.Request) {
	server := p.NextServer()
	proxy := httputil.NewSingleHostReverseProxy(server)
	proxy.ServeHTTP(w, r)
}

var pool ServerPool

func Run() {
	servers := []string{
		"http://localhost:8081",
		"http://localhost:8082",
		"http://localhost:8083",
	}

	for _, server := range servers {
		url, err := url.Parse(server)
		if err != nil {
			log.Fatalf("Failed to parse server URL: %v", err)
		}
		pool.AddServer(url)
	}

	http.HandleFunc("/", pool.LoadBalance)
	fmt.Println("Load balancer started on :8080")
	log.Fatal(http.ListenAndServe(":8080", nil))
}

```

## Step 4: Create the `main.go` File

Create a `main.go` file to start the load balancer.

```go
// main.go
package main

import "github.com/username/loadbalancer/lib"

func main() {
	lib.Run()
}

```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go
```

This will start the load balancer on port 8080, balancing requests across the servers specified in the `servers` slice.