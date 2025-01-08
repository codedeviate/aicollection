# IP Geolocation

To create an IP geolocation program in Go, you need to create a few files: `main.go` for the main logic and optionally, a `geolocation.go` file for the geolocation functionality. Here is a step-by-step guide:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir ipgeolocation
cd ipgeolocation
go mod init github.com/username/ipgeolocation
```

## Step 2: Create the `geolocation.go` File

Create a `geolocation/geolocation.go` file to handle the IP geolocation functionality.

```go
// geolocation.go
package geolocation

import (
	"encoding/json"
	"fmt"
	"net/http"
)

type Geolocation struct {
    IP          string  `json:"ip"`
    Country     string  `json:"country_name"`
    Region      string  `json:"region_name"`
    City        string  `json:"city"`
    Latitude    float64 `json:"latitude"`
    Longitude   float64 `json:"longitude"`
    Timezone    string  `json:"time_zone"`
}

func GetGeolocation(ip string) (*Geolocation, error) {
    url := fmt.Sprintf("https://freegeoip.app/json/%s", ip)
    resp, err := http.Get(url)
    if err != nil {
        return nil, err
    }
    defer resp.Body.Close()

    var geo Geolocation
    if err := json.NewDecoder(resp.Body).Decode(&geo); err != nil {
        return nil, err
    }

    return &geo, nil
}

```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the geolocation functionality.

```go
// main.go
package main

import (
	"fmt"
	"os"

	"github.com/username/ipgeolocation/geolocation"
)

func main() {
	if len(os.Args) != 2 {
		fmt.Println("Usage: ipgeolocation <ip>")
		os.Exit(1)
	}

	ip := os.Args[1]
	geo, err := geolocation.GetGeolocation(ip)
	if err != nil {
		fmt.Printf("Failed to get geolocation: %v\n", err)
		os.Exit(1)
	}

	fmt.Printf("IP: %s\nCountry: %s\nRegion: %s\nCity: %s\nLatitude: %f\nLongitude: %f\nTimezone: %s\n",
		geo.IP, geo.Country, geo.Region, geo.City, geo.Latitude, geo.Longitude, geo.Timezone)
}

```

## Step 4: Run the Program

Run the program using the `go run` command.

```sh
go run main.go 8.8.8.8
```

This will fetch and display the geolocation information for the specified IP address.