# Hexdump

Here's a Go program to create a simple **hexdump** utility. The program will be divided into logical files and modules for better organization. The utility reads a file and displays its contents in hexadecimal, ASCII, and offsets.

## Project Structure
```
hexdump/
├── go.mod
├── main.go
├── lib/
│   ├── hexdump.go
│   ├── formatter.go
│   └── reader.go
```

## Step-by-Step Implementation

### 1. Initialize the Go Project
Run the following commands:
```bash
mkdir hexdump
cd hexdump
mkdir lib
go mod init hexdump
```

---

### 2. Create `main.go`
This is the entry point of the application.

```go
package main

import (
	"flag"
	"fmt"
	"os"

	"github.com/username/hexdump/lib"
)

func main() {
	// Parse command-line arguments
	filePath := flag.String("file", "", "Path to the file to hexdump")
	flag.Parse()

	if *filePath == "" {
		fmt.Println("Usage: hexdump -file <path-to-file>")
		os.Exit(1)
	}

	// Open the file
	file, err := os.Open(*filePath)
	if err != nil {
		fmt.Printf("Error opening file: %v\n", err)
		os.Exit(1)
	}
	defer file.Close()

	// Perform the hexdump
	if err := lib.Dump(file, os.Stdout); err != nil {
		fmt.Printf("Error performing hexdump: %v\n", err)
		os.Exit(1)
	}
}
```

---

### 3. Create `lib/hexdump.go`
This file orchestrates the hexdump logic.

```go
package lib

import (
	"io"
)

// Dump reads from the input reader and writes a formatted hexdump to the output writer.
func Dump(input io.Reader, output io.Writer) error {
	reader := NewReader(input)
	formatter := NewFormatter()

	var baseCount int64 = 0

	for {
		offset, data, err := reader.ReadChunk()
		if err == io.EOF {
			break
		} else if err != nil {
			return err
		}

		line := formatter.Format(baseCount, data)
		baseCount += offset
		_, err = output.Write([]byte(line))
		if err != nil {
			return err
		}
	}
	return nil
}
```

---

### 4. Create `lib/reader.go`
This file handles reading chunks of data from the file.

```go
package hexdump

import (
	"io"
)

const chunkSize = 16

type Reader struct {
	input io.Reader
}

func NewReader(input io.Reader) *Reader {
	return &Reader{input: input}
}

func (r *Reader) ReadChunk() (int64, []byte, error) {
	buffer := make([]byte, chunkSize)
	n, err := r.input.Read(buffer)
	if n == 0 {
		return 0, nil, err
	}
	return int64(n), buffer[:n], err
}
```

---

### 5. Create `lib/formatter.go`
This file handles formatting the data into a hexdump format.

```go
package hexdump

import (
	"fmt"
	"strings"
)

type Formatter struct{}

func NewFormatter() *Formatter {
	return &Formatter{}
}

func (f *Formatter) Format(offset int64, data []byte) string {
	hexPart := make([]string, len(data))
	asciiPart := make([]rune, len(data))

	for i, b := range data {
		hexPart[i] = fmt.Sprintf("%02x", b)
		if b >= 32 && b <= 126 {
			asciiPart[i] = rune(b)
		} else {
			asciiPart[i] = '.'
		}
	}

	return fmt.Sprintf("%08x  %-48s  |%s|\n", offset, strings.Join(hexPart, " "), string(asciiPart))
}
```

---

## How It Works
1. **`main.go`**: Parses the command-line argument for the file path and calls `lib.Dump`.
2. **`hexdump.go`**: Manages the flow of reading and formatting chunks of data.
3. **`reader.go`**: Reads the file in fixed-size chunks.
4. **`formatter.go`**: Formats each chunk into a hexdump format with offset, hexadecimal values, and ASCII representation.

---

## Running the Program
1. Build the program:
   ```bash
   go build -o hexdump
   ```

2. Run the program with a file:
   ```bash
   ./hexdump -file example.txt
   ```

This modular structure allows easy maintenance and scaling for additional features (e.g., support for different encodings or output formats).