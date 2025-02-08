# Dynamic Portspoof Application

*Crafting a Dynamic Portspoof Application in Go with External Configuration*

> **Disclaimer:** The code presented here is intended solely for research, educational, and testing purposes. Always ensure you have proper authorization before deploying any network deception tools.

In today’s cybersecurity landscape, deception tools are often employed to misdirect and study attacker behavior. In this tutorial, we’ll build a portspoof application in Go that fakes multiple network services on configurable ports. Each fake service responds with a custom banner, logs connection attempts, supports both IPv4/IPv6 and TLS encryption, and even provides an interactive experience. With an external JSON configuration file, you can easily choose which ports to open, which service to emulate, and what messages to display.

## Key Features

- **External Configuration:** Define ports, service types, and custom banners in a JSON file.
- **Multi-Service Emulation:** Support for fake SSH, HTTP, MySQL, and generic services.
- **Custom Responses:** Each service sends a configurable banner upon connection.
- **Per-Service Logging:** Events are logged into individual files (e.g., `ssh.log`, `http.log`).
- **IPv6 & TLS Support:** Bind to `[::]` for dual-stack support and optionally wrap connections with TLS.
- **Interactive Sessions:** Simulate basic interactive sessions that echo attacker input.
- **Alerting & Dashboard:** Track suspicious IP activity and display recent events via a simple real-time HTTP dashboard.

---

## Project Directory Structure

The project is organized into several packages to keep the code modular and maintainable:

```
portspoof/
├── alerts/
│   └── alert.go          // Monitors suspicious activity and issues alerts.
├── config/
│   ├── config.go         // Loads settings from an external JSON file.
│   └── config.json       // External configuration file with service definitions.
├── dashboard/
│   └── dashboard.go      // Provides a simple HTTP dashboard to monitor events.
├── logging/
│   └── logger.go         // Utility for service-specific logging.
├── network/
│   └── listener.go       // Sets up network listeners for each configured service.
├── services/
│   ├── fake_http.go      // Emulates a fake HTTP service.
│   ├── fake_mysql.go     // Emulates a fake MySQL service.
│   ├── fake_service.go   // Common interactive behavior for fake services.
│   └── fake_ssh.go       // Emulates a fake SSH service.
├── utils/
│   └── random.go         // Random utility functions.
└── main.go               // Application entry point.
```

---

## Step 1. Creating the External Configuration File

Create a JSON file (`config/config.json`) to define which ports to listen on, which service to emulate on each, and the corresponding custom banner. For example:

```json
{
  "services": [
    { "port": 2222, "service": "ssh", "banner": "SSH-2.0-OpenSSH_7.9 (Fake)" },
    { "port": 8080, "service": "http", "banner": "HTTP/1.1 200 OK\r\nContent-Type: text/html\r\n\r\n<html><body><h1>Fake HTTP Service</h1></body></html>" },
    { "port": 3306, "service": "mysql", "banner": "5.7.0-MySQL Community Server (Fake)" },
    { "port": 9001, "service": "generic", "banner": "Welcome to fake service on port 9001" }
  ],
  "tlsCertFile": "cert.pem",
  "tlsKeyFile": "key.pem",
  "dashboardPort": 9000,
  "suspiciousThreshold": 5
}
```

This file lets you easily modify which services are active and customize their responses without touching the code.

---

## Step 2. Writing the Code

### 2.1 Main Entry Point

The `main.go` file initializes the configuration, starts the dashboard, and spins up the network listeners based on the external settings.

```go
// main.go
package main

import (
	"fmt"
	"log"
	"os"
	"os/signal"
	"portspoof/config"
	"portspoof/dashboard"
	"portspoof/network"
	"syscall"
)

func main() {
	// Load settings from the external configuration file.
	cfg, err := config.LoadConfig("config/config.json")
	if err != nil {
		log.Fatalf("Error loading configuration: %v", err)
	}

	log.Println("Starting Portspoof Service...")

	// Start the real-time dashboard on a separate goroutine.
	go func() {
		if err := dashboard.StartDashboard(cfg.DashboardPort); err != nil {
			log.Fatalf("Dashboard failed: %v", err)
		}
	}()

	// Launch network listeners based on external configuration.
	go network.StartListeners(cfg)

	// Wait for termination signal (e.g., Ctrl+C).
	sigs := make(chan os.Signal, 1)
	signal.Notify(sigs, syscall.SIGINT, syscall.SIGTERM)
	<-sigs

	fmt.Println("Shutting down Portspoof...")
}
```

---

### 2.2 External Configuration Loader

The configuration package reads settings from the JSON file.

```go
// config/config.go
package config

import (
	"encoding/json"
	"fmt"
	"io/ioutil"
	"os"
)

// PortService defines a service on a specific port.
type PortService struct {
	Port    int    `json:"port"`
	Service string `json:"service"` // "ssh", "http", "mysql", "generic"
	Banner  string `json:"banner"`  // Custom banner for the service.
}

// Config holds the entire configuration.
type Config struct {
	Services            []PortService `json:"services"`
	TLSCertFile         string        `json:"tlsCertFile"`
	TLSKeyFile          string        `json:"tlsKeyFile"`
	DashboardPort       int           `json:"dashboardPort"`
	SuspiciousThreshold int           `json:"suspiciousThreshold"`
}

// LoadConfig reads the configuration from a JSON file.
func LoadConfig(path string) (Config, error) {
	var cfg Config

	file, err := os.Open(path)
	if err != nil {
		return cfg, fmt.Errorf("could not open config file %s: %v", path, err)
	}
	defer file.Close()

	data, err := ioutil.ReadAll(file)
	if err != nil {
		return cfg, fmt.Errorf("error reading config file: %v", err)
	}

	if err := json.Unmarshal(data, &cfg); err != nil {
		return cfg, fmt.Errorf("error parsing config file: %v", err)
	}
	return cfg, nil
}
```

---

### 2.3 Logging Utility

Each service logs its connection events into its own file. The logging package handles this in a thread-safe manner.

```go
// logging/logger.go
package logging

import (
	"fmt"
	"log"
	"os"
	"sync"
	"time"
)

var (
	loggers = make(map[string]*log.Logger)
	mu      sync.Mutex
)

// getLogger returns (or creates) a logger for a given service.
func getLogger(service string) *log.Logger {
	mu.Lock()
	defer mu.Unlock()

	if logger, exists := loggers[service]; exists {
		return logger
	}

	// Create or append to a log file named after the service.
	fileName := fmt.Sprintf("%s.log", service)
	file, err := os.OpenFile(fileName, os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0644)
	if err != nil {
		log.Fatalf("Unable to open log file %s: %v", fileName, err)
	}
	logger := log.New(file, fmt.Sprintf("[%s] ", service), log.LstdFlags)
	loggers[service] = logger
	return logger
}

// LogEvent writes an event string to the appropriate log file.
func LogEvent(service, event string) {
	logger := getLogger(service)
	logger.Printf("%s - %s", time.Now().Format(time.RFC3339), event)
}
```

---

### 2.4 Alerting for Suspicious Activity

The alerts package monitors connection counts per IP address. When an IP exceeds the configured threshold, an alert is logged and printed.

```go
// alerts/alert.go
package alerts

import (
	"fmt"
	"sync"
	"time"
	"portspoof/logging"
)

var (
	ipActivity = make(map[string]int)
	mu         sync.Mutex
	threshold  = 5 // Default; can be overridden from config.
)

// SetThreshold configures the threshold for suspicious activity.
func SetThreshold(t int) {
	mu.Lock()
	defer mu.Unlock()
	threshold = t
}

// RecordActivity increments the connection count for an IP.
func RecordActivity(ip string) {
	mu.Lock()
	defer mu.Unlock()

	ipActivity[ip]++
	if ipActivity[ip] >= threshold {
		triggerAlert(ip, ipActivity[ip])
		// Reset after issuing an alert.
		ipActivity[ip] = 0
	}
}

// triggerAlert logs and prints an alert message.
func triggerAlert(ip string, count int) {
	alertMsg := fmt.Sprintf("Suspicious activity from IP %s: %d attempts", ip, count)
	logging.LogEvent("alerts", alertMsg)
	fmt.Println("ALERT:", alertMsg)
}
```

---

### 2.5 Real-Time Dashboard

A simple HTTP server displays recent events in JSON format. This dashboard can be extended with more advanced interfaces or WebSocket support.

```go
// dashboard/dashboard.go
package dashboard

import (
	"encoding/json"
	"fmt"
	"log"
	"net/http"
	"sync"
	"time"
)

// DashboardEvent represents a single event record.
type DashboardEvent struct {
	Time     time.Time `json:"time"`
	Service  string    `json:"service"`
	Message  string    `json:"message"`
	RemoteIP string    `json:"remote_ip"`
}

var (
	events []DashboardEvent
	mu     sync.Mutex
)

// AddEvent appends an event to the dashboard log.
func AddEvent(event DashboardEvent) {
	mu.Lock()
	defer mu.Unlock()
	events = append(events, event)
	if len(events) > 100 {
		events = events[len(events)-100:]
	}
}

// StartDashboard runs an HTTP server that returns recent events as JSON.
func StartDashboard(port int) error {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		mu.Lock()
		defer mu.Unlock()
		w.Header().Set("Content-Type", "application/json")
		json.NewEncoder(w).Encode(events)
	})
	addr := fmt.Sprintf(":%d", port)
	log.Printf("Dashboard available at http://localhost%s", addr)
	return http.ListenAndServe(addr, nil)
}
```

---

### 2.6 Utility Functions

The `random.go` utility offers functions to help randomize choices (for example, deciding whether to enable TLS on a service).

```go
// utils/random.go
package utils

import (
	"math/rand"
	"time"
)

func init() {
	rand.Seed(time.Now().UnixNano())
}

// RandomChoice returns a random element from a slice.
func RandomChoice(choices []string) string {
	return choices[rand.Intn(len(choices))]
}
```

---

### 2.7 Base Fake Service Implementation

The base fake service provides the common interactive behavior: sending a banner, reading attacker input, logging, and echoing responses.

```go
// services/fake_service.go
package services

import (
	"bufio"
	"crypto/tls"
	"fmt"
	"net"
	"portspoof/alerts"
	"portspoof/dashboard"
	"portspoof/logging"
	"strings"
	"time"
)

// Service is the interface for a fake service.
type Service interface {
	Handle(conn net.Conn, remoteIP string)
	Banner() string
}

// GenericService implements common functionality for fake services.
type GenericService struct {
	serviceName string
	banner      string
	useTLS      bool
	tlsConfig   *tls.Config
}

// NewGenericService creates a new GenericService.
func NewGenericService(name, banner string, useTLS bool, tlsConfig *tls.Config) *GenericService {
	return &GenericService{
		serviceName: name,
		banner:      banner,
		useTLS:      useTLS,
		tlsConfig:   tlsConfig,
	}
}

// Banner returns the configured banner.
func (s *GenericService) Banner() string {
	return s.banner
}

// Handle processes a connection: sends a banner, logs input, and echoes responses.
func (s *GenericService) Handle(conn net.Conn, remoteIP string) {
	defer conn.Close()

	logging.LogEvent(s.serviceName, fmt.Sprintf("Connection from %s", remoteIP))
	dashboard.AddEvent(dashboard.DashboardEvent{
		Time:     time.Now(),
		Service:  s.serviceName,
		Message:  "New connection",
		RemoteIP: remoteIP,
	})

	if s.useTLS {
		if tlsConn, ok := conn.(*tls.Conn); ok {
			if err := tlsConn.Handshake(); err != nil {
				logging.LogEvent(s.serviceName, fmt.Sprintf("TLS handshake error from %s: %v", remoteIP, err))
				return
			}
		}
	}

	// Send the fake banner.
	conn.Write([]byte(s.Banner() + "\n"))

	scanner := bufio.NewScanner(conn)
	for scanner.Scan() {
		input := scanner.Text()
		logging.LogEvent(s.serviceName, fmt.Sprintf("Input from %s: %s", remoteIP, input))
		dashboard.AddEvent(dashboard.DashboardEvent{
			Time:     time.Now(),
			Service:  s.serviceName,
			Message:  "Received input: " + input,
			RemoteIP: remoteIP,
		})
		alerts.RecordActivity(remoteIP)
		// Echo back a simple response.
		response := strings.ToUpper(input)
		conn.Write([]byte("Echo: " + response + "\n"))
	}
}
```

---

### 2.8 Specialized Fake Services

Each specific fake service (SSH, HTTP, MySQL) is a thin wrapper around the base service that can override the default banner if needed.

**Fake SSH Service:**

```go
// services/fake_ssh.go
package services

import (
	"crypto/tls"
)

// FakeSSHService simulates an SSH service.
type FakeSSHService struct {
	*GenericService
}

// NewFakeSSHService returns a new FakeSSHService.
func NewFakeSSHService(customBanner string, useTLS bool, tlsConfig *tls.Config) *FakeSSHService {
	banner := customBanner
	if banner == "" {
		banner = "SSH-2.0-OpenSSH_7.4 (Fake)"
	}
	return &FakeSSHService{
		GenericService: NewGenericService("ssh", banner, useTLS, tlsConfig),
	}
}
```

**Fake HTTP Service:**

```go
// services/fake_http.go
package services

import (
	"crypto/tls"
)

// FakeHTTPService simulates an HTTP service.
type FakeHTTPService struct {
	*GenericService
}

// NewFakeHTTPService returns a new FakeHTTPService.
func NewFakeHTTPService(customBanner string, useTLS bool, tlsConfig *tls.Config) *FakeHTTPService {
	banner := customBanner
	if banner == "" {
		banner = "HTTP/1.1 200 OK\r\nContent-Type: text/html\r\n\r\n<html><body><h1>Fake HTTP Service</h1></body></html>"
	}
	return &FakeHTTPService{
		GenericService: NewGenericService("http", banner, useTLS, tlsConfig),
	}
}
```

**Fake MySQL Service:**

```go
// services/fake_mysql.go
package services

import (
	"crypto/tls"
)

// FakeMySQLService simulates a MySQL service.
type FakeMySQLService struct {
	*GenericService
}

// NewFakeMySQLService returns a new FakeMySQLService.
func NewFakeMySQLService(customBanner string, useTLS bool, tlsConfig *tls.Config) *FakeMySQLService {
	banner := customBanner
	if banner == "" {
		banner = "5.7.0-MySQL Community Server (Fake)"
	}
	return &FakeMySQLService{
		GenericService: NewGenericService("mysql", banner, useTLS, tlsConfig),
	}
}
```

---

### 2.9 Network Listener Setup

Finally, the network package reads the configuration and sets up listeners on the defined ports. It instantiates the appropriate fake service for each port and optionally wraps the listener in TLS.

```go
// network/listener.go
package network

import (
	"crypto/tls"
	"fmt"
	"log"
	"math/rand"
	"net"
	"os"
	"portspoof/config"
	"portspoof/services"
	"portspoof/utils"
	"strconv"
)

// StartListeners creates a listener for every service defined in the config.
func StartListeners(cfg config.Config) {
	// Load shared TLS configuration if available.
	tlsConfig, err := loadTLSConfig(cfg.TLSCertFile, cfg.TLSKeyFile)
	if err != nil {
		log.Printf("TLS configuration load error: %v. TLS will be disabled.", err)
		tlsConfig = nil
	}

	for _, ps := range cfg.Services {
		// Randomly decide whether to use TLS (if available) for this service.
		useTLS := (rand.Intn(2) == 0) && (tlsConfig != nil)

		var svc services.Service
		switch ps.Service {
		case "ssh":
			svc = services.NewFakeSSHService(ps.Banner, useTLS, tlsConfig)
		case "http":
			svc = services.NewFakeHTTPService(ps.Banner, useTLS, tlsConfig)
		case "mysql":
			svc = services.NewFakeMySQLService(ps.Banner, useTLS, tlsConfig)
		default:
			banner := ps.Banner
			if banner == "" {
				banner = fmt.Sprintf("Welcome to fake service on port %d", ps.Port)
			}
			svc = services.NewGenericService("generic", banner, useTLS, tlsConfig)
		}
		go startListener(ps.Port, svc, useTLS, tlsConfig)
	}
}

// startListener binds to the given port and services incoming connections.
func startListener(port int, svc services.Service, useTLS bool, tlsConfig *tls.Config) {
	addr := "[::]:" + strconv.Itoa(port)
	var ln net.Listener
	var err error

	if useTLS && tlsConfig != nil {
		ln, err = tls.Listen("tcp", addr, tlsConfig)
	} else {
		ln, err = net.Listen("tcp", addr)
	}
	if err != nil {
		log.Printf("Error listening on %s: %v", addr, err)
		return
	}
	log.Printf("Listening on %s for service %s (TLS: %v)", addr, svc.Banner(), useTLS)

	for {
		conn, err := ln.Accept()
		if err != nil {
			log.Printf("Accept error on port %d: %v", port, err)
			continue
		}
		remoteIP, _, _ := net.SplitHostPort(conn.RemoteAddr().String())
		go svc.Handle(conn, remoteIP)
	}
}

// loadTLSConfig attempts to load the TLS certificate and key.
func loadTLSConfig(certFile, keyFile string) (*tls.Config, error) {
	if _, err := os.Stat(certFile); os.IsNotExist(err) {
		return nil, fmt.Errorf("TLS certificate file %s not found", certFile)
	}
	cert, err := tls.LoadX509KeyPair(certFile, keyFile)
	if err != nil {
		return nil, err
	}
	return &tls.Config{Certificates: []tls.Certificate{cert}}, nil
}
```

---

## Running the Portspoof Application

1. **Prepare the Configuration:**  
   Edit `config/config.json` with the desired ports, service types, and banners.

2. **(Optional) Generate TLS Certificates:**  
   If you wish to enable TLS for some services, generate a self-signed certificate with:
   ```bash
   openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
   ```

3. **Build the Application:**  
   From the project root, compile the program:
   ```bash
   go build -o portspoof .
   ```

4. **Run the Application:**  
   Launch the executable:
   ```bash
   ./portspoof
   ```

5. **Test the Deceptive Services:**  
   Use tools like `telnet` or `nc` to connect to one of the configured ports (for example, port 2222 for SSH). You should see the custom banner you defined. Meanwhile, visit [http://localhost:9000](http://localhost:9000) to view the real-time dashboard displaying recent events.

---

## Conclusion

In this tutorial, you learned how to build a sophisticated portspoof application in Go that uses an external configuration file to determine its behavior. By decoupling the service definitions from the code, you can rapidly adjust the deception tactics, experiment with different banners, and observe attacker behavior in real time. This modular design leverages Go’s strong concurrency and networking capabilities, making it an ideal starting point for more advanced deception systems.

Happy coding, and remember to use these techniques responsibly!