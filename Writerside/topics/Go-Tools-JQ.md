# JQ

The `jq` tool is a lightweight and flexible command-line JSON processor. It allows you to extract, transform, and manipulate JSON data using a simple and expressive query language. In this guide, we'll explore how to use `jq` to work with JSON data in various ways. But instead of just being able to read `json`, this tools will also be able to read and process `xml` data.

To create a `jq`-like program in Go that can parse CSV, JSON, and XML, and read from both file and stdin, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir jq_program
cd jq_program
go mod init github.com/username/jq_program
```

## Step 2: Install Dependencies

You will need the following libraries:
- `github.com/tidwall/gjson` for JSON parsing
- `github.com/clbanning/mxj` for XML parsing
- `github.com/jszwec/csvutil` for CSV parsing

```sh
go get github.com/tidwall/gjson
go get github.com/clbanning/mxj
go get github.com/jszwec/csvutil
```

## Step 3: Create the `jq.go` File

Create a `jq.go` file to handle the JSON, XML, and CSV functionality.

```go
// jq.go
package main

import (
    "encoding/csv"
    "fmt"
    "github.com/clbanning/mxj"
    "github.com/jszwec/csvutil"
    "github.com/tidwall/gjson"
    "io"
    "os"
)

// ProcessJSON processes JSON input and applies a query.
func ProcessJSON(jsonData, query string) string {
    result := gjson.Get(jsonData, query)
    return result.String()
}

// ProcessXML processes XML input and applies a query.
func ProcessXML(xmlData, query string) string {
    mv, err := mxj.NewMapXml([]byte(xmlData))
    if err != nil {
        return fmt.Sprintf("Error parsing XML: %v", err)
    }

    result, err := mv.ValueForPath(query)
    if err != nil {
        return fmt.Sprintf("Error querying XML: %v", err)
    }

    return fmt.Sprintf("%v", result)
}

// ProcessCSV processes CSV input and applies a query.
func ProcessCSV(csvData, query string) string {
    var records []map[string]interface{}
    if err := csvutil.Unmarshal([]byte(csvData), &records); err != nil {
        return fmt.Sprintf("Error parsing CSV: %v", err)
    }

    for _, record := range records {
        if value, ok := record[query]; ok {
            return fmt.Sprintf("%v", value)
        }
    }
    return "Query not found"
}

// ReadFile reads the content of a file.
func ReadFile(filePath string) (string, error) {
    data, err := os.ReadFile(filePath)
    if err != nil {
        return "", err
    }
    return string(data), nil
}

// ReadStdin reads the content from standard input.
func ReadStdin() (string, error) {
    data, err := io.ReadAll(os.Stdin)
    if err != nil {
        return "", err
    }
    return string(data), nil
}
```

## Step 4: Create the `main.go` File

Create a `main.go` file to use the JSON, XML, and CSV functionality.

```go
// main.go
package main

import (
    "flag"
    "fmt"
    "os"
)

func main() {
    file := flag.String("file", "", "Path to the file (CSV, JSON, or XML)")
    query := flag.String("query", "", "Query to apply to the data")
    format := flag.String("format", "json", "Format of the input data (csv, json, or xml)")
    flag.Parse()

    if *query == "" {
        fmt.Println("Usage: jq_program --file <file_path> --query <query> --format <csv|json|xml>")
        os.Exit(1)
    }

    var data string
    var err error

    if *file != "" {
        data, err = ReadFile(*file)
        if err != nil {
            fmt.Printf("Error reading file: %v\n", err)
            os.Exit(1)
        }
    } else {
        data, err = ReadStdin()
        if err != nil {
            fmt.Printf("Error reading stdin: %v\n", err)
            os.Exit(1)
        }
    }

    var result string
    switch *format {
    case "json":
        result = ProcessJSON(data, *query)
    case "xml":
        result = ProcessXML(data, *query)
    case "csv":
        result = ProcessCSV(data, *query)
    default:
        fmt.Println("Unsupported format. Use 'csv', 'json', or 'xml'.")
        os.Exit(1)
    }

    fmt.Println(result)
}
```

## Step 5: Run the Program

Run the program using the `go run` command.

To read JSON from a file:

```sh
go run main.go --file example.json --query "key.nestedKey" --format json
```

To read XML from a file:

```sh
go run main.go --file example.xml --query "key.nestedKey" --format xml
```

To read CSV from a file:

```sh
go run main.go --file example.csv --query "columnName" --format csv
```

To read JSON from standard input:

```sh
cat example.json | go run main.go --query "key.nestedKey" --format json
```

To read XML from standard input:

```sh
cat example.xml | go run main.go --query "key.nestedKey" --format xml
```

To read CSV from standard input:

```sh
cat example.csv | go run main.go --query "columnName" --format csv
```

Replace `example.json`, `example.xml`, or `example.csv` with the path to your file and `key.nestedKey` or `columnName` with your desired query. This will parse the JSON, XML, or CSV data and extract the value based on the query.