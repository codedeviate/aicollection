# Compression

## Building a Modular Compression Program in Go

In this article, we will create a modular compression program in Go that supports **Gzip**, **Zlib**, **Deflate**, **LZW**, and **Snappy**. The program will be divided into logical files for better organization, and each module will handle a specific compression format.

### Goals of the Program
1. Learn how different compression algorithms work in Go.
2. Use Go's standard library for supported formats (Gzip, Zlib, Deflate, and LZW).
3. Use an external package (`github.com/golang/snappy`) for Snappy compression.

---

## Code Structure
We will divide the program into the following files:
1. `main.go` - Entry point and CLI logic.
2. `gzip.go` - Handles Gzip compression and decompression.
3. `zlib.go` - Handles Zlib compression and decompression.
4. `deflate.go` - Handles Deflate compression and decompression.
5. `lzw.go` - Handles LZW compression and decompression.
6. `snappy.go` - Handles Snappy compression and decompression.

---

## Step-by-Step Implementation

### 1. `main.go`
Handles CLI inputs and routes to the appropriate compression module.

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	if len(os.Args) < 4 {
		fmt.Println("Usage: go run main.go <compress|decompress> <format> <file>")
		return
	}

	action := os.Args[1]
	format := os.Args[2]
	file := os.Args[3]

	switch format {
	case "gzip":
		handleGzip(action, file)
	case "zlib":
		handleZlib(action, file)
	case "deflate":
		handleDeflate(action, file)
	case "lzw":
		handleLzw(action, file)
	case "snappy":
		handleSnappy(action, file)
	default:
		fmt.Println("Unsupported format. Supported formats: gzip, zlib, deflate, lzw, snappy")
	}
}
```

---

### 2. `gzip.go`
Handles Gzip compression and decompression.

```go
package main

import (
	"compress/gzip"
	"fmt"
	"io"
	"os"
)

func handleGzip(action, file string) {
	switch action {
	case "compress":
		compressGzip(file)
	case "decompress":
		decompressGzip(file)
	default:
		fmt.Println("Invalid action. Use 'compress' or 'decompress'.")
	}
}

func compressGzip(file string) {
	inFile, err := os.Open(file)
	if err != nil {
		fmt.Println("Error opening file:", err)
		return
	}
	defer inFile.Close()

	outFile, err := os.Create(file + ".gz")
	if err != nil {
		fmt.Println("Error creating output file:", err)
		return
	}
	defer outFile.Close()

	writer := gzip.NewWriter(outFile)
	defer writer.Close()

	_, err = io.Copy(writer, inFile)
	if err != nil {
		fmt.Println("Error compressing file:", err)
	}
	fmt.Println("File compressed to", file+".gz")
}

func decompressGzip(file string) {
	inFile, err := os.Open(file)
	if err != nil {
		fmt.Println("Error opening file:", err)
		return
	}
	defer inFile.Close()

	outFile, err := os.Create(file[:len(file)-3]) // Remove ".gz"
	if err != nil {
		fmt.Println("Error creating output file:", err)
		return
	}
	defer outFile.Close()

	reader, err := gzip.NewReader(inFile)
	if err != nil {
		fmt.Println("Error creating gzip reader:", err)
		return
	}
	defer reader.Close()

	_, err = io.Copy(outFile, reader)
	if err != nil {
		fmt.Println("Error decompressing file:", err)
	}
	fmt.Println("File decompressed to", outFile.Name())
}
```

---

### 3. `zlib.go`
Handles Zlib compression and decompression.

```go
package main

import (
	"compress/zlib"
	"fmt"
	"io"
	"os"
)

func handleZlib(action, file string) {
	switch action {
	case "compress":
		compressZlib(file)
	case "decompress":
		decompressZlib(file)
	default:
		fmt.Println("Invalid action. Use 'compress' or 'decompress'.")
	}
}

func compressZlib(file string) {
	inFile, err := os.Open(file)
	if err != nil {
		fmt.Println("Error opening file:", err)
		return
	}
	defer inFile.Close()

	outFile, err := os.Create(file + ".zlib")
	if err != nil {
		fmt.Println("Error creating output file:", err)
		return
	}
	defer outFile.Close()

	writer := zlib.NewWriter(outFile)
	defer writer.Close()

	_, err = io.Copy(writer, inFile)
	if err != nil {
		fmt.Println("Error compressing file:", err)
	}
	fmt.Println("File compressed to", file+".zlib")
}

func decompressZlib(file string) {
	inFile, err := os.Open(file)
	if err != nil {
		fmt.Println("Error opening file:", err)
		return
	}
	defer inFile.Close()

	outFile, err := os.Create(file[:len(file)-5]) // Remove ".zlib"
	if err != nil {
		fmt.Println("Error creating output file:", err)
		return
	}
	defer outFile.Close()

	reader, err := zlib.NewReader(inFile)
	if err != nil {
		fmt.Println("Error creating zlib reader:", err)
		return
	}
	defer reader.Close()

	_, err = io.Copy(outFile, reader)
	if err != nil {
		fmt.Println("Error decompressing file:", err)
	}
	fmt.Println("File decompressed to", outFile.Name())
}
```

---

### 4. `deflate.go`
Handles Deflate compression and decompression.

```go
package main

import (
	"compress/flate"
	"fmt"
	"io"
	"os"
)

func handleDeflate(action, file string) {
	switch action {
	case "compress":
		compressDeflate(file)
	case "decompress":
		decompressDeflate(file)
	default:
		fmt.Println("Invalid action. Use 'compress' or 'decompress'.")
	}
}

func compressDeflate(file string) {
	inFile, err := os.Open(file)
	if err != nil {
		fmt.Println("Error opening file:", err)
		return
	}
	defer inFile.Close()

	outFile, err := os.Create(file + ".deflate")
	if err != nil {
		fmt.Println("Error creating output file:", err)
		return
	}
	defer outFile.Close()

	writer, err := flate.NewWriter(outFile, flate.DefaultCompression)
	if err != nil {
		fmt.Println("Error creating deflate writer:", err)
		return
	}
	defer writer.Close()

	_, err = io.Copy(writer, inFile)
	if err != nil {
		fmt.Println("Error compressing file:", err)
	}
	fmt.Println("File compressed to", file+".deflate")
}

func decompressDeflate(file string) {
	inFile, err := os.Open(file)
	if err != nil {
		fmt.Println("Error opening file:", err)
		return
	}
	defer inFile.Close()

	outFile, err := os.Create(file[:len(file)-8]) // Remove ".deflate"
	if err != nil {
		fmt.Println("Error creating output file:", err)
		return
	}
	defer outFile.Close()

	reader := flate.NewReader(inFile)
	defer reader.Close()

	_, err = io.Copy(outFile, reader)
	if err != nil {
		fmt.Println("Error decompressing file:", err)
	}
	fmt.Println("File decompressed to", outFile.Name())
}
```

---

## 5. `lzw.go`
Handles LZW compression and decompression.

```go
package main

import (
	"compress/lzw"
	"fmt"
	"io"
	"os"
)

func handleLzw(action, file string) {
	switch action {
	case "compress":
		compressLzw(file)
	case "decompress":
		decompressLzw(file)
	default:
		fmt.Println("Invalid action. Use 'compress' or 'decompress'.")
	}
}

func compressLzw(file string) {
	inFile, err := os.Open(file)
	if err != nil {
		fmt.Println("Error opening file:", err)
		return
	}
	defer inFile.Close()

	outFile, err := os.Create(file + ".lzw")
	if err != nil {
		fmt.Println("Error creating output file:", err)
		return
	}
	defer outFile.Close()

	// Use LSB (least significant bit) order
	writer := lzw.NewWriter(outFile, lzw.LSB, 8)
	defer writer.Close()

	_, err = io.Copy(writer, inFile)
	if err != nil {
		fmt.Println("Error compressing file:", err)
	}
	fmt.Println("File compressed to", file+".lzw")
}

func decompressLzw(file string) {
	inFile, err := os.Open(file)
	if err != nil {
		fmt.Println("Error opening file:", err)
		return
	}
	defer inFile.Close()

	outFile, err := os.Create(file[:len(file)-4]) // Remove ".lzw"
	if err != nil {
		fmt.Println("Error creating output file:", err)
		return
	}
	defer outFile.Close()

	// Use LSB (least significant bit) order
	reader := lzw.NewReader(inFile, lzw.LSB, 8)
	defer reader.Close()

	_, err = io.Copy(outFile, reader)
	if err != nil {
		fmt.Println("Error decompressing file:", err)
	}
	fmt.Println("File decompressed to", outFile.Name())
}
```

---

## 6. `snappy.go`
Handles Snappy compression and decompression. This requires the `github.com/golang/snappy` package, so make sure to install it:

```bash
go get github.com/golang/snappy
```

```go
package main

import (
	"fmt"
	"github.com/golang/snappy"
	"io"
	"os"
)

func handleSnappy(action, file string) {
	switch action {
	case "compress":
		compressSnappy(file)
	case "decompress":
		decompressSnappy(file)
	default:
		fmt.Println("Invalid action. Use 'compress' or 'decompress'.")
	}
}

func compressSnappy(file string) {
	inFile, err := os.Open(file)
	if err != nil {
		fmt.Println("Error opening file:", err)
		return
	}
	defer inFile.Close()

	outFile, err := os.Create(file + ".snappy")
	if err != nil {
		fmt.Println("Error creating output file:", err)
		return
	}
	defer outFile.Close()

	writer := snappy.NewBufferedWriter(outFile)
	defer writer.Close()

	_, err = io.Copy(writer, inFile)
	if err != nil {
		fmt.Println("Error compressing file:", err)
	}
	fmt.Println("File compressed to", file+".snappy")
}

func decompressSnappy(file string) {
	inFile, err := os.Open(file)
	if err != nil {
		fmt.Println("Error opening file:", err)
		return
	}
	defer inFile.Close()

	outFile, err := os.Create(file[:len(file)-7]) // Remove ".snappy"
	if err != nil {
		fmt.Println("Error creating output file:", err)
		return
	}
	defer outFile.Close()

	reader := snappy.NewReader(inFile)

	_, err = io.Copy(outFile, reader)
	if err != nil {
		fmt.Println("Error decompressing file:", err)
	}
	fmt.Println("File decompressed to", outFile.Name())
}
```

---

## Testing the Program

1. **Run the Program:**
   ```bash
   go run main.go compress gzip test.txt
   go run main.go decompress gzip test.txt.gz
   ```

2. **Test All Formats:**
   Replace `gzip` with `zlib`, `deflate`, `lzw`, or `snappy` to test other formats.

3. **Expected Results:**
    - Compressed files will have appropriate extensions (`.gz`, `.zlib`, `.deflate`, `.lzw`, `.snappy`).
    - Decompressed files will match the original input.

---

## Conclusion
This modular program allows you to compress and decompress files using popular algorithms. Each module is self-contained, enabling you to focus on learning and extending individual algorithms as needed. The full code can be extended to include more algorithms or features such as streaming or error handling improvements.