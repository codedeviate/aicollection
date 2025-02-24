# Log Analyzer

To create a log analyzer program in Go that can process log files for Apache2, Nginx, and MySQL/MariaDB, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir log_analyzer
cd log_analyzer
go mod init github.com/username/log_analyzer
```

## Step 2: Create the `analyzer.go` File

Create an `lib/analyzer.go` file to handle the log processing functionality.

```go
// analyzer.go
package lib

import (
	"bufio"
	"os"
	"regexp"
)

// LogEntry represents a parsed log entry.
type LogEntry struct {
	RemoteAddress string
	Client        string
	User          string
	Timestamp     string
	Message       string
}

// ProcessApacheAccessLog processes Apache2 access log entries.
func ProcessApacheAccessLog(line string) LogEntry {
	re := regexp.MustCompile(`([0-9a-f\.\:]+)\s(.*)\s(.*)\s\[(.*?)\] (.*)`)
	matches := re.FindStringSubmatch(line)
	if len(matches) == 6 {
		return LogEntry{
			RemoteAddress: matches[1],
			Client:        matches[2],
			User:          matches[3],
			Timestamp:     matches[4],
			Message:       matches[5],
		}
	}
	return LogEntry{}
}

// ProcessApacheErrorLog processes Apache2 error log entries.
func ProcessApacheErrorLog(line string) LogEntry {
	re := regexp.MustCompile(`\[(.*?)\] \[(.*?)\] \[(.*?)\] (.*)`)
	matches := re.FindStringSubmatch(line)
	if len(matches) == 5 {
		return LogEntry{Timestamp: matches[1], Message: matches[4]}
	}
	return LogEntry{}
}

// ProcessNginxAccessLog processes Nginx access log entries.
func ProcessNginxAccessLog(line string) LogEntry {
	re := regexp.MustCompile(`\[(.*?)\] (.*)`)
	matches := re.FindStringSubmatch(line)
	if len(matches) == 3 {
		return LogEntry{Timestamp: matches[1], Message: matches[2]}
	}
	return LogEntry{}
}

// ProcessNginxErrorLog processes Nginx error log entries.
func ProcessNginxErrorLog(line string) LogEntry {
	re := regexp.MustCompile(`\[(.*?)\] \[(.*?)\] (.*)`)
	matches := re.FindStringSubmatch(line)
	if len(matches) == 4 {
		return LogEntry{Timestamp: matches[1], Message: matches[3]}
	}
	return LogEntry{}
}

// ProcessMySQLLog processes MySQL/MariaDB log entries.
func ProcessMySQLLog(line string) LogEntry {
	re := regexp.MustCompile(`(\d{6} \d{2}:\d{2}:\d{2}) (.*)`)
	matches := re.FindStringSubmatch(line)
	if len(matches) == 3 {
		return LogEntry{Timestamp: matches[1], Message: matches[2]}
	}
	return LogEntry{}
}

// ReadFile reads the content of a file line by line.
func ReadFile(filePath string, processFunc func(string) LogEntry) ([]LogEntry, error) {
	file, err := os.Open(filePath)
	if err != nil {
		return nil, err
	}
	defer file.Close()

	var entries []LogEntry
	scanner := bufio.NewScanner(file)
	for scanner.Scan() {
		line := scanner.Text()
		entry := processFunc(line)
		if entry.Timestamp != "" {
			entries = append(entries, entry)
		}
	}
	return entries, scanner.Err()
}

```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the log processing functionality.

```go
// main.go
package main

import (
	"flag"
	"fmt"
	"os"

	"github.com/username/loganalyzer/lib"
)

func main() {
	file := flag.String("file", "", "Path to the log file")
	logType := flag.String("type", "apache_access", "Log type (apache_access, apache_error, nginx_access, nginx_error, mysql)")
	flag.Parse()

	if *file == "" {
		fmt.Println("Usage: loganalyzer --file <log_file> --type <apache_access|apache_error|nginx_access|nginx_error|mysql>")
		os.Exit(1)
	}

	var processFunc func(string) lib.LogEntry
	switch *logType {
	case "apache_access":
		processFunc = lib.ProcessApacheAccessLog
	case "apache_error":
		processFunc = lib.ProcessApacheErrorLog
	case "nginx_access":
		processFunc = lib.ProcessNginxAccessLog
	case "nginx_error":
		processFunc = lib.ProcessNginxErrorLog
	case "mysql":
		processFunc = lib.ProcessMySQLLog
	default:
		fmt.Println("Unsupported log type. Use 'apache_access', 'apache_error', 'nginx_access', 'nginx_error', or 'mysql'.")
		os.Exit(1)
	}

	entries, err := lib.ReadFile(*file, processFunc)
	if err != nil {
		fmt.Printf("Error reading file: %v\n", err)
		os.Exit(1)
	}

	for _, entry := range entries {
		fmt.Printf("[%s] %s\n", entry.Timestamp, entry.Message)
		if entry.Client != "" && entry.Client != "-" {
			fmt.Printf("  Client: %s\n", entry.Client)
		}
		if entry.RemoteAddress != "" && entry.RemoteAddress != "-" {
			fmt.Printf("  RemoteAddress: %s\n", entry.RemoteAddress)
		}
		if entry.User != "" && entry.User != "-" {
			fmt.Printf("  User: %s\n", entry.User)
		}
	}
}

```

## Step 4: Run the Program

Run the program using the `go run` command.

To process an Apache2 log file:

```sh
go run main.go --file apache.log --type apache
```

To process an Nginx log file:

```sh
go run main.go --file nginx.log --type nginx
```

To process a MySQL/MariaDB log file:

```sh
go run main.go --file mysql.log --type mysql
```

Replace `apache.log`, `nginx.log`, or `mysql.log` with the path to your log file. This will process the log entries and print the parsed results.