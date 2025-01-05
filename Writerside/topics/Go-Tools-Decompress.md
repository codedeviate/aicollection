# Decompression

## Building a Multi-Format File Unpacking Utility in Go

In this article, we'll walk you through building a utility in Go that can unpack various file compression formats like `.zip`, `.rar`, `.7z`, and more. We'll aim to create a modular, easy-to-extend application that handles these different compression formats in separate packages. The program will allow users to specify a compressed file, and the utility will automatically unpack it to the desired location.

### Project Overview

The goal of this utility is to:
1. Accept a compressed file (such as `.zip`, `.rar`, `.7z`, etc.) as input.
2. Detect the file type based on its extension.
3. Use the appropriate unpacking method to extract the file's contents.
4. Print the status and extracted files.

We will break the project into multiple modules:
- **Main program** (`main.go`): Entry point to handle user input.
- **Unpacker module** (`unpacker/unpacker.go`): Logic to detect and unpack files.
- **Utility module** (`utils/utils.go`): Helper functions, such as checking file types and validating paths.

### Project Structure

```
file-unpacker/
│
├── main.go              // Entry point of the program
├── unpacker/            // Module for unpacking files
│   ├── zip.go           // Logic to unpack .zip files
│   ├── rar.go           // Logic to unpack .rar files
│   └── sevenzip.go      // Logic to unpack .7z files
└── utils/               // Utility functions
    └── utils.go         // Helper functions (e.g., checking file types)
```

### Step-by-Step Guide

#### 1. Initialize the Go Project

The first step in setting up the project is to initialize the Go module.

```bash
go mod init file-unpacker
```

This creates a Go module that manages dependencies.

#### 2. Unpacker Module

The `unpacker` module will contain different files to handle each compression format. Each file will implement the logic for unpacking that format. We will implement unpackers for `.zip`, `.rar`, and `.7z` files.

##### 2.1 ZIP Unpacker (`unpacker/zip.go`)

This file will handle the extraction of `.zip` files.

```go
// unpacker/zip.go
package unpacker

import (
	"archive/zip"
	"fmt"
	"io"
	"os"
	"path/filepath"
)

// Unzip extracts a .zip file to the specified destination folder.
func Unzip(src string, dest string) error {
	// Open the zip file
	zipFile, err := zip.OpenReader(src)
	if err != nil {
		return fmt.Errorf("failed to open zip file: %v", err)
	}
	defer zipFile.Close()

	// Iterate over the files in the archive
	for _, file := range zipFile.File {
		err := extractZipFile(file, dest)
		if err != nil {
			return err
		}
	}
	return nil
}

// extractZipFile extracts a single file from the zip archive.
func extractZipFile(file *zip.File, dest string) error {
	// Open the file inside the zip archive
	rc, err := file.Open()
	if err != nil {
		return fmt.Errorf("failed to open file inside zip: %v", err)
	}
	defer rc.Close()

	// Prepare the destination file path
	destPath := filepath.Join(dest, file.Name)

	// Create the necessary directories if they don't exist
	if file.FileInfo().IsDir() {
		err = os.MkdirAll(destPath, file.Mode())
		if err != nil {
			return fmt.Errorf("failed to create directory: %v", err)
		}
	} else {
		// Create the destination file
		destFile, err := os.Create(destPath)
		if err != nil {
			return fmt.Errorf("failed to create file: %v", err)
		}
		defer destFile.Close()

		// Copy the content from the zip file to the destination file
		_, err = io.Copy(destFile, rc)
		if err != nil {
			return fmt.Errorf("failed to copy file content: %v", err)
		}
	}
	return nil
}
```

##### 2.2 RAR Unpacker (`unpacker/rar.go`)

To unpack `.rar` files, we can use the `github.com/nwaples/rardecode` package. You'll need to install this package using:

```bash
go get github.com/nwaples/rardecode
```

Here’s the unpacking logic for `.rar` files:

```go
// unpacker/rar.go
package unpacker

import (
	"fmt"
	"github.com/nwaples/rardecode"
	"io"
	"os"
	"path/filepath"
)

// Unrar extracts a .rar file to the specified destination folder.
func Unrar(src string, dest string) error {
	// Open the rar file
	file, err := os.Open(src)
	if err != nil {
		return fmt.Errorf("failed to open rar file: %v", err)
	}
	defer file.Close()

	// Create a new rar reader
	r, err := rardecode.NewReader(file, "")
	if err != nil {
		return fmt.Errorf("failed to create rar reader: %v", err)
	}

	// Extract files from the rar archive
	for {
		header, err := r.Next()
		if err == io.EOF {
			break
		}
		if err != nil {
			return fmt.Errorf("failed to read next file: %v", err)
		}

		// Extract each file
		err = extractRarFile(header, r, dest)
		if err != nil {
			return err
		}
	}
	return nil
}

// extractRarFile extracts a single file from the rar archive.
func extractRarFile(header *rardecode.FileHeader, r *rardecode.Reader, dest string) error {
	destPath := filepath.Join(dest, header.Name)

	// Create the destination file
	destFile, err := os.Create(destPath)
	if err != nil {
		return fmt.Errorf("failed to create file: %v", err)
	}
	defer destFile.Close()

	// Copy the content from the rar file to the destination file
	_, err = io.Copy(destFile, r)
	if err != nil {
		return fmt.Errorf("failed to copy file content: %v", err)
	}
	return nil
}
```

##### 2.3 7z Unpacker (`unpacker/sevenzip.go`)

For `.7z` files, we will use the `github.com/mholt/archiver/v3` package. Install it using:

```bash
go get github.com/mholt/archiver/v3
```

Here’s how to handle `.7z` files:

```go
// unpacker/sevenzip.go
package unpacker

import (
	"fmt"
	"github.com/mholt/archiver/v3"
)

// Un7z extracts a .7z file to the specified destination folder.
func Un7z(src string, dest string) error {
	// Use the archiver package to extract the .7z file
	err := archiver.Unarchive(src, dest)
	if err != nil {
		return fmt.Errorf("failed to unpack .7z file: %v", err)
	}
	return nil
}
```

#### 3. Utility Module: `utils/utils.go`

The `utils` module contains helper functions for file path validation and type checking.

```go
// utils/utils.go
package utils

import (
	"strings"
)

// GetExtension checks the file extension of the given file.
func GetExtension(filePath string) string {
	return strings.ToLower(strings.TrimPrefix(strings.ToLower(filePath), "."))
}

// IsZip checks if the file is a .zip file.
func IsZip(filePath string) bool {
	return GetExtension(filePath) == "zip"
}

// IsRar checks if the file is a .rar file.
func IsRar(filePath string) bool {
	return GetExtension(filePath) == "rar"
}

// Is7z checks if the file is a .7z file.
func Is7z(filePath string) bool {
	return GetExtension(filePath) == "7z"
}
```

#### 4. Main Program: `main.go`

The `main.go` file is the entry point, responsible for accepting user input and calling the appropriate unpacker function.

```go
// main.go
package main

import (
	"fmt"
	"os"
	"path/filepath"
	"file-unpacker/unpacker"   // Import unpacker module
	"file-unpacker/utils"      // Import utils module
)

func main() {
	if len(os.Args) < 3 {
		fmt.Println("Usage: go run main.go <file-path> <destination-folder>")
		os.Exit(1)
	}

	filePath := os.Args[1]
	destFolder := os.Args[2]

	// Check the file type and call the appropriate unpacking function
	switch {
	case utils.IsZip(filePath):
		err := unpacker.Unzip(filePath, destFolder)
		if err != nil {
			fmt.Println("Error unpacking zip file:", err)
		} else {
			fmt.Println("Successfully unpacked zip file!")
		}
	case utils.IsRar(filePath):
		err := unpacker.Unrar(filePath, destFolder)
		if err != nil {
			fmt.Println("Error unpacking rar file:", err)
		} else {
			fmt.Println("Successfully unpacked rar file!")
		}
	case utils.Is7z(filePath):
		err := unpacker.Un7z(filePath, destFolder)
		if err != nil {
			fmt.Println("Error unpacking 7z file:", err)
		} else {
			fmt.Println("Successfully unpacked 7z file!")
		}
	default:
		fmt.Println("Unsupported file format:", filePath)
	}
}
```

### Running the Program

Once the program is complete, you can run it using:

```bash
go run main.go <compressed-file-path> <destination-folder>
```

### Example

```bash
go run main.go example.zip ./extracted
```

This will unpack the `.zip` file into the `./extracted` folder.

### Conclusion

In this article, we created a Go-based utility capable of unpacking various compression formats such as `.zip`, `.rar`, and `.7z`. The program was modularized into separate packages to handle the different file formats and provided utility functions to validate and extract files. This modular structure allows for easy extension to support additional formats in the future.