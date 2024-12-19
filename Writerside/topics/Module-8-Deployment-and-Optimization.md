# Module 8: Deployment and Optimization

## Detailed Topics:

### Deployment:
Deployment involves preparing your Go application to run in a production environment. Key steps include creating Docker images, configuring container orchestration, and ensuring scalability and reliability. Topics covered include:

1. **Packaging with Docker**:
    - Write a `Dockerfile` to containerize your Go application.
    - Understand multi-stage builds to optimize image size.
    - Example:
      ```Docker
      # Stage 1: Build the application
      FROM golang:1.20 AS builder
      WORKDIR /app
      COPY . .
      RUN go build -o myapp
 
      # Stage 2: Create a minimal runtime image
      FROM alpine:latest
      WORKDIR /root/
      COPY --from=builder /app/myapp .
      CMD ["./myapp"]
      ```

2. **Deployment Strategies**:
    - Manual vs automated deployments.
    - Using Docker Compose or Kubernetes for multi-container applications.
    - Deploying on cloud platforms like AWS, GCP, or Azure.

### Optimization:
Optimization ensures your Go application performs efficiently under load. This involves profiling, debugging, and making iterative improvements. Topics include:

1. **Profiling with `pprof`**:
    - Collect CPU, memory, and goroutine profiles.
    - Visualize profiling data to identify bottlenecks.
    - Example:
      ```go
      package main
 
      import (
          "log"
          "net/http"
          _ "net/http/pprof"
      )
 
      func main() {
          go func() {
              log.Println(http.ListenAndServe("localhost:6060", nil))
          }()
          // Your application code here
      }
      ```

2. **Debugging Performance Issues**:
    - Use `trace` to monitor execution latency and runtime events.
    - Leverage tools like `dlv` (Delve) for runtime debugging.

## Detailed Hands-On:

### 1. Containerize a Go Web Server and Deploy It:
- Create a simple Go web server:
  ```go
  package main

  import (
      "fmt"
      "net/http"
  )

  func handler(w http.ResponseWriter, r *http.Request) {
      fmt.Fprintf(w, "Hello, World!")
  }

  func main() {
      http.HandleFunc("/", handler)
      http.ListenAndServe(":8080", nil)
  }
  ```
- Write a `Dockerfile` to containerize the server (as shown above).
- Run the container locally:
  ```bash
  docker build -t my-go-server .
  docker run -p 8080:8080 my-go-server
  ```
- Deploy to a cloud platform (e.g., AWS ECS or Google Cloud Run).

### 2. Analyze Performance Bottlenecks Using Profiling Tools:
- Profile a sample Go application:
  ```go
  package main

  import (
      "math"
      "time"
  )

  func compute() {
      for i := 0; i < 1e6; i++ {
          _ = math.Sqrt(float64(i))
      }
  }

  func main() {
      for {
          compute()
          time.Sleep(1 * time.Second)
      }
  }
  ```
- Run the application with profiling enabled:
  ```bash
  go run -cpuprofile=cpu.prof main.go
  ```
- Analyze the profile using `pprof`:
  ```bash
  go tool pprof cpu.prof
  ```
  Example commands within `pprof`:
    - `top`: Show the most time-consuming functions.
    - `web`: Visualize the call graph.

- Use `trace` for advanced analysis:
  ```bash
  go run -trace=trace.out main.go
  go tool trace trace.out
  ```

