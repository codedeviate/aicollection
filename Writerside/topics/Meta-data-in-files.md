# Executable header formats

Executable file headers are integral components of executable files, containing crucial metadata that defines how a file should be loaded and executed by the operating system. These headers specify the file's type, architecture, entry points, sections, and more, serving as the roadmap for the OS to interpret the file correctly. Understanding these headers is essential for software developers, reverse engineers, and cybersecurity professionals.

This article provides a high-level overview of various executable file header formats. It acts as an introduction to more specific articles detailing individual formats such as ELF, PE, Mach-O, and more.

---

## What Are Executable File Headers?

An executable file header is the first part of an executable file. It contains metadata and instructions that help the operating system understand the file’s contents and purpose. Key components of most headers include:

- **Magic Numbers**: Unique identifiers that distinguish different file formats.
- **Machine Type**: Information about the target architecture (e.g., x86, x86-64, ARM).
- **Entry Point**: The starting address of the program's execution.
- **Section Headers**: Information about various sections like code, data, and resources.

Headers are typically structured differently across formats but serve similar purposes.

---

## Common Executable File Formats

Here is a summary of popular executable file formats and their characteristics:

### 1. ELF (Executable and Linkable Format)
- **Used By**: Unix-based systems such as Linux and FreeBSD.
- **Features**:
    - Supports 32-bit and 64-bit architectures.
    - Includes a flexible design for dynamic linking and loading.
    - Contains sections like `.text` (code) and `.data` (initialized data).
- **Header Components**:
    - Magic number: `\x7fELF`
    - Machine type: Indicates architecture, such as `EM_X86_64` for 64-bit.

### 2. PE (Portable Executable)
- **Used By**: Microsoft Windows.
- **Features**:
    - Derived from the COFF (Common Object File Format).
    - Supports dynamic linking through DLLs.
    - Includes sections for code, data, resources, and imports.
- **Header Components**:
    - DOS stub: Starts with `MZ`.
    - PE signature: `PE\x00\x00`.
    - Optional header: Specifies whether the file is 32-bit or 64-bit.

### 3. Mach-O (Mach Object)
- **Used By**: macOS and iOS.
- **Features**:
    - Designed for dynamic linking and efficient loading.
    - Flexible enough to support multiple architectures (fat binaries).
- **Header Components**:
    - Magic numbers: `\xca\xfe\xba\xbe` for 32-bit and `\xfe\xed\xfa\xcf` for 64-bit.
    - Load commands: Define segments and dynamic libraries.

### 4. DOS Executable (MZ)
- **Used By**: DOS and as a stub for PE files.
- **Features**:
    - Simple format for early executable files.
    - Often includes a PE offset for modern Windows executables.
- **Header Components**:
    - Magic number: `MZ`.
    - Fields for relocation information and code offset.

### 5. COFF (Common Object File Format)
- **Used By**: Older Unix systems and as a basis for PE.
- **Features**:
    - Designed for object files rather than executables.
    - Includes section headers for relocations and symbol tables.

### 6. a.out (Assembler Output)
- **Used By**: Early Unix systems.
- **Features**:
    - Predecessor to ELF.
    - Limited flexibility compared to modern formats.
- **Header Components**:
    - Magic numbers indicating architecture.

### 7. XCOFF (Extended COFF)
- **Used By**: IBM’s AIX operating system.
- **Features**:
    - Extends COFF to support dynamic linking and other modern features.
    - Contains additional metadata for compatibility with AIX tools.

### 8. LE/LX (Linear Executable)
- **Used By**: OS/2.
- **Features**:
    - Provides advanced capabilities over MZ.
    - Supports dynamic linking and flat memory models.

### 9. PEF (Preferred Executable Format)
- **Used By**: Classic Mac OS.
- **Features**:
    - Designed for efficient loading on PowerPC architectures.
    - Includes resources for managing memory and code segments.

---

## How Headers Are Analyzed

Analyzing executable file headers typically involves:

1. **Reading the Header**: Load the first few bytes of the file to examine magic numbers and key fields.
2. **Parsing Metadata**: Use the file’s documented structure to extract relevant details.
3. **Identifying the Format**: Match magic numbers and other key fields to known formats.

For example, a Go program might read the first 64 bytes of a file to identify its format using logic like:

```go
func identifyFileType(header []byte) string {
	switch {
	case string(header[:4]) == "\x7fELF":
		return "ELF"
	case string(header[:2]) == "MZ":
		return "DOS Executable or PE"
	case string(header[:4]) == "PE\x00\x00":
		return "Portable Executable (PE)"
	default:
		return "Unknown format"
	}
}
```

---

## Conclusion

Executable file headers are the key to understanding how different operating systems and architectures handle binary files. By studying these headers, we can gain insight into file formats, enabling tasks like compatibility checks, reverse engineering, and malware analysis.

Each format offers unique features and challenges. Detailed articles on individual formats like ELF, PE, and Mach-O will explore their headers, fields, and use cases more thoroughly.

