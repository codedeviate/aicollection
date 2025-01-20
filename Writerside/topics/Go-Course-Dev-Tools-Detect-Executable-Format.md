# Building a Go Program to Identify Executable File Formats

Executable files are core components in computing, representing machine-readable instructions that the operating system
can execute. In this article, we'll walk through creating a Go program to read executable files and interpret their
headers to determine the file type and architecture. This tutorial is designed with beginners in mind, so we'll break
down every step of the process and provide detailed explanations of the concepts involved.

## What We Will Build
Our program will analyze the headers of executable files to identify their type and architecture. It will support
detecting the following formats:

- ELF (Executable and Linkable Format) - ELF32 and ELF64
- Mach-O (Mach Object) - 32-bit and 64-bit
- PE (Portable Executable) - 32-bit and 64-bit
- DOS Executable (MZ)

### Prerequisites
Before starting, ensure you have the following:

1. **Go Installed**: Download and install Go from [golang.org](https://golang.org/dl/).
2. **Basic Understanding of Go**: Familiarity with Go syntax and concepts like functions, structs, and error handling will be helpful.

---

## Step 1: Creating the Project Structure

Start by creating a new folder for your project. Inside this folder, create a main file:

```bash
mkdir executable-inspector
cd executable-inspector
touch main.go
```

---

## Step 2: Reading the Executable File

First, we need to read the contents of the file. Go provides an excellent `os` package for working with files.

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	if len(os.Args) < 2 {
		fmt.Println("Usage:", os.Args[0], "main.go <file_path>")
		return
	}

	filePath := os.Args[1]
	file, err := os.Open(filePath)
	if err != nil {
		fmt.Printf("Error opening file: %v\n", err)
		return
	}
	defer file.Close()

	header := make([]byte, 0x100)
	_, err = file.Read(header)
	if err != nil {
		fmt.Printf("Error reading file header: %v\n", err)
		return
	}

	fmt.Println("File Type:", identifyFileType(header))
}
```

### Explanation of main
1. **os.Args**: This is used to fetch command-line arguments. The first argument is the program's name, so the second argument is the file path.
2. **os.Open**: Opens the file for reading. We handle errors using Go's idiomatic `if err != nil` pattern.
3. **defer**: Ensures that the file is closed when the function exits.

---

## Step 3: Identifying the File Type

Each file format has a unique signature (magic number) at the beginning of its header. The updated function to identify
the file type is as follows:

```go
func identifyFileType(header []byte) string {
	switch {
	case string(header[:4]) == "\x7fELF":
		return identifyELF(header)
	case string(header[:2]) == "MZ":
		return identifyDOS(header)
	case string(header[:4]) == "PE\x00\x00":
		return "Portable Executable (PE)"
	case string(header[:4]) == "\xca\xfe\xba\xbe":
		return "Mach-O 32-bit"
	case string(header[:4]) == "\xbe\xba\xfe\xca":
		return "Mach-O 32-bit"
	case string(header[:4]) == "\xfe\xed\xfa\xcf":
		return "Mach-O 64-bit"
	case string(header[:4]) == "\xcf\xfa\xed\xfe":
		return "Mach-O 64-bit"
	default:
		fmt.Printf("%X %X %X %X\n", header[0], header[1], header[2], header[3])
		return "Unknown format"
	}
}
```

### Explanation of File Type Identification
1. **Magic Numbers**: Expanded to include more cases for Mach-O files with reversed byte orders (e.g., `\xbe\xba\xfe\xca`).
2. **Fallback**: Prints the first four bytes in hexadecimal if the format is unrecognized.

---

## Step 4: Handling Specific Formats

### Identifying ELF Files
```go
func identifyELF(header []byte) string {
	if header[4] == 1 {
		return "ELF 32-bit"
	} else if header[4] == 2 {
		return "ELF 64-bit"
	}
	return "Unknown ELF type"
}
```

### Identifying DOS Executables
```go
func identifyDOS(header []byte) string {
	peOffset := int(header[0x3c])
	if string(header[peOffset:peOffset+4]) == "PE\x00\x00" {
		archType := string(header[peOffset+4 : peOffset+6])
		if archType == "\x64\x86" {
			return "Portable Executable (PE) 64-bit"
		} else if archType == "\x4c\x01" {
			return "Portable Executable (PE) 32-bit"
		}
		optionalHeaderSize := int(header[peOffset+20])
		if optionalHeaderSize == 224 {
			return "Portable Executable (PE) 32-bit"
		} else if optionalHeaderSize == 240 {
			return "Portable Executable (PE) 64-bit"
		}
		return "Portable Executable (PE)"
	}
	return "DOS Executable (MZ)"
}
```

### Explanation of DOS and PE Identification
1. **PE Offset**: Found at byte `0x3C` in the DOS header and used to locate the PE signature.
2. **Architecture Check**: The architecture type is determined by bytes after the PE signature.
3. **Optional Header Size**: Helps distinguish between 32-bit and 64-bit PE files.

---

## Step 5: Putting It All Together

Here is the complete updated code:

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	if len(os.Args) < 2 {
		fmt.Println("Usage: go run main.go <file_path>")
		return
	}

	filePath := os.Args[1]
	file, err := os.Open(filePath)
	if err != nil {
		fmt.Printf("Error opening file: %v\n", err)
		return
	}
	defer file.Close()

	header := make([]byte, 0x100)
	_, err = file.Read(header)
	if err != nil {
		fmt.Printf("Error reading file header: %v\n", err)
		return
	}

	fmt.Println("File Type:", identifyFileType(header))
}

func identifyFileType(header []byte) string {
	switch {
	case string(header[:4]) == "\x7fELF":
		return identifyELF(header)
	case string(header[:2]) == "MZ":
		return identifyDOS(header)
	case string(header[:4]) == "PE\x00\x00":
		return "Portable Executable (PE)"
	case string(header[:4]) == "\xca\xfe\xba\xbe":
		return "Mach-O 32-bit"
	case string(header[:4]) == "\xbe\xba\xfe\xca":
		return "Mach-O 32-bit"
	case string(header[:4]) == "\xfe\xed\xfa\xcf":
		return "Mach-O 64-bit"
	case string(header[:4]) == "\xcf\xfa\xed\xfe":
		return "Mach-O 64-bit"
	default:
		fmt.Printf("%X %X %X %X\n", header[0], header[1], header[2], header[3])
		return "Unknown format"
	}
}

func identifyELF(header []byte) string {
	if header[4] == 1 {
		return "ELF 32-bit"
	} else if header[4] == 2 {
		return "ELF 64-bit"
	}
	return "Unknown ELF type"
}

func identifyDOS(header []byte) string {
	peOffset := int(header[0x3c])
	if string(header[peOffset:peOffset+4]) == "PE\x00\x00" {
		archType := string(header[peOffset+4 : peOffset+6])
		if archType == "\x64\x86" {
			return "Portable Executable (PE) 64-bit"
		} else if archType == "\x4c\x01" {
			return "Portable Executable (PE) 32-bit"
		}
		optionalHeaderSize := int(header[peOffset+20])
		if optionalHeaderSize == 224 {
			return "Portable Executable (PE) 32-bit"
		} else if optionalHeaderSize == 240 {
			return "Portable Executable (PE) 64-bit"
		}
		return "Portable Executable (PE)"
	}
	return "DOS Executable (MZ)"
}
```


### Conclusion of Code Integration
The code has the ability to identify ELF, Mach-O, and DOS/PE file formats. By running the program with the `go run`
command and providing a valid executable file path, you can determine the file's format and architecture.