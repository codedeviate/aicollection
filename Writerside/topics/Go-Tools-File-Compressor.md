# File Compressor

To create a file compressor program in Go, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir filecompressor
cd filecompressor
go mod init github.com/username/filecompressor
```

## Step 2: Install Dependencies

You will need the `compress/gzip` package for Gzip compression.

## Step 3: Create the `compressor.go` File

Create a `lib/compressor.go` file to handle the compression and decompression functionality.

```go
// compressor.go
package lib

import (
	"compress/gzip"
	"io"
	"os"
)

// CompressFile compresses the given file using Gzip.
func CompressFile(source, target string) error {
    srcFile, err := os.Open(source)
    if err != nil {
        return err
    }
    defer srcFile.Close()

    tgtFile, err := os.Create(target)
    if err != nil {
        return err
    }
    defer tgtFile.Close()

    writer := gzip.NewWriter(tgtFile)
    defer writer.Close()

    _, err = io.Copy(writer, srcFile)
    return err
}

// DecompressFile decompresses the given Gzip file.
func DecompressFile(source, target string) error {
    srcFile, err := os.Open(source)
    if err != nil {
        return err
    }
    defer srcFile.Close()

    reader, err := gzip.NewReader(srcFile)
    if err != nil {
        return err
    }
    defer reader.Close()

    tgtFile, err := os.Create(target)
    if err != nil {
        return err
    }
    defer tgtFile.Close()

    _, err = io.Copy(tgtFile, reader)
    return err
}

```

## Step 4: Create the `main.go` File

Create a `main.go` file to use the compression and decompression functionality.

```go
// main.go
package main

import (
	"flag"
	"fmt"
	"os"

	"github.com/username/filecompressor/lib"
)

func main() {
	compress := flag.Bool("compress", false, "Compress the file")
	decompress := flag.Bool("decompress", false, "Decompress the file")
	source := flag.String("source", "", "Source file path")
	target := flag.String("target", "", "Target file path")
	flag.Parse()

	if *source == "" || *target == "" {
		fmt.Println("Usage: file_compressor --compress|--decompress --source <source_file> --target <target_file>")
		os.Exit(1)
	}

	var err error
	if *compress {
		err = lib.CompressFile(*source, *target)
	} else if *decompress {
		err = lib.DecompressFile(*source, *target)
	} else {
		fmt.Println("Specify either --compress or --decompress")
		os.Exit(1)
	}

	if err != nil {
		fmt.Printf("Operation failed: %v\n", err)
		os.Exit(1)
	}

	fmt.Println("Operation successful")
}

```

## Step 5: Run the Program

Run the program using the `go run` command.

To compress a file:

```sh
go run main.go --compress --source example.txt --target example.txt.gz
```

To decompress a file:

```sh
go run main.go --decompress --source example.txt.gz --target example.txt
```

Replace `example.txt` and `example.txt.gz` with the paths to your source and target files. This will compress or decompress the file as specified.