# Encode/Decode

To create a program in Go that can encode and decode Base64 and URL, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir encoder_decoder
cd encoder_decoder
mkdir lib
go mod init github.com/username/encoder_decoder
```

## Step 2: Create the `encoder.go` File

Create an `lib/encodedecode.go` file to handle the encoding and decoding functionality.

```go
// encodedecode.go
package lib

import (
	"encoding/base64"
	"net/url"
)

// Base64Encode encodes a string to Base64.
func Base64Encode(data string) string {
	return base64.StdEncoding.EncodeToString([]byte(data))
}

// Base64Decode decodes a Base64 string.
func Base64Decode(data string) (string, error) {
	decoded, err := base64.StdEncoding.DecodeString(data)
	if err != nil {
		return "", err
	}
	return string(decoded), nil
}

// URLEncode encodes a string to URL encoding.
func URLEncode(data string) string {
	return url.QueryEscape(data)
}

// URLDecode decodes a URL encoded string.
func URLDecode(data string) (string, error) {
	decoded, err := url.QueryUnescape(data)
	if err != nil {
		return "", err
	}
	return decoded, nil
}

```

## Step 3: Create the `main.go` File

Create a `main.go` file to use the encoding and decoding functionality.

```go
package main

import (
	"bufio"
	"flag"
	"fmt"
	"io"
	"os"

	"github.com/username/encodedecode/lib"
)

func main() {
	mode := flag.String("mode", "encode", "Mode: encode or decode")
	method := flag.String("method", "base64", "Method: base64 or url")
	input := flag.String("input", "", "Input string")
	filePath := flag.String("file", "", "Path to input file")
	flag.Parse()

	var data string
	if *filePath != "" {
		// Read from file
		file, err := os.Open(*filePath)
		if err != nil {
			fmt.Printf("Error opening file: %v\n", err)
			os.Exit(1)
		}
		defer file.Close()
		reader := bufio.NewReader(file)
		inputBytes, err := io.ReadAll(reader)
		if err != nil {
			fmt.Printf("Error reading file: %v\n", err)
			os.Exit(1)
		}
		data = string(inputBytes)
	} else if *input == "" {
		// Check if input is coming from a pipe
		fi, err := os.Stdin.Stat()
		if err != nil {
			fmt.Printf("Error: %v\n", err)
			os.Exit(1)
		}

		if fi.Mode()&os.ModeNamedPipe != 0 {
			// Read from stdin
			reader := bufio.NewReader(os.Stdin)
			inputBytes, err := io.ReadAll(reader)
			if err != nil {
				fmt.Printf("Error reading from stdin: %v\n", err)
				os.Exit(1)
			}
			data = string(inputBytes)
		} else {
			fmt.Println("Enter input string:")
			scanner := bufio.NewScanner(os.Stdin)
			if scanner.Scan() {
				data = scanner.Text()
			}
		}
	} else {
		data = *input
	}

	var result string
	var err error

	switch *method {
	case "base64":
		if *mode == "encode" {
			result = lib.Base64Encode(data)
		} else {
			result, err = lib.Base64Decode(data)
		}
	case "url":
		if *mode == "encode" {
			result = lib.URLEncode(data)
		} else {
			result, err = lib.URLDecode(data)
		}
	default:
		fmt.Println("Unsupported method. Use 'base64' or 'url'.")
		os.Exit(1)
	}

	if err != nil {
		fmt.Printf("Error: %v\n", err)
		os.Exit(1)
	}

	fmt.Println(result)
}

```

## Step 4: Run the Program

Run the program using the `go run` command.

To encode a string to Base64:

```sh
go run main.go --mode encode --method base64 --input "Hello, World!"
```

To decode a Base64 string:

```sh
go run main.go --mode decode --method base64 --input "SGVsbG8sIFdvcmxkIQ=="
```

To encode a string to URL encoding:

```sh
go run main.go --mode encode --method url --input "Hello, World!"
```

To decode a URL encoded string:

```sh
go run main.go --mode decode --method url --input "Hello%2C+World%21"
```

This will encode or decode the input string based on the specified mode and method.

### Example for Piped Data

To encode data piped from another command to Base64:

```sh
echo "Hello, World!" | go run main.go --mode encode --method base64
```

To decode Base64 data piped from another command:

```sh
echo "SGVsbG8sIFdvcmxkIQ==" | go run main.go --mode decode --method base64
```

To encode data piped from another command to URL encoding:

```sh
echo "Hello, World!" | go run main.go --mode encode --method url
```

To decode URL encoded data piped from another command:

```sh
echo "Hello%2C+World%21" | go run main.go --mode decode --method url
```

### Example for Data Read from File

To encode data read from a file to Base64:

```sh
go run main.go --mode encode --method base64 --file path/to/input.txt
```

To decode Base64 data read from a file:

```sh
go run main.go --mode decode --method base64 --file path/to/input.txt
```

To encode data read from a file to URL encoding:

```sh
go run main.go --mode encode --method url --file path/to/input.txt
```

To decode URL encoded data read from a file:

```sh
go run main.go --mode decode --method url --file path/to/input.txt
```

### Example with default values

The default mode is `encode` and the default method is `base64`. If no input is provided, the program will prompt for input.

To enter input manually:

```sh
go run main.go
```

To base64 encode a file:

```sh
cat path/to/input.txt | go run main.go
```