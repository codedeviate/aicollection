# LX (Linear Executable Format)

LX is the Linear Executable format, an extension of the LE format, used primarily in OS/2 2.x and later. It supports 32-bit addressing and advanced features like demand paging and dynamic linking, making it suitable for modern multitasking operating systems. Here's a breakdown of what the LX header contains and how you can find where the code begins:

---

## Structure of the LX Header

The LX header typically contains the following fields:

1. **Magic Number**:
    - The first four bytes of the file are `LX` (0x4C 0x58), which identifies the file as a Linear Executable.

2. **Header Fields**:
    - **`ByteOrder`** (1 byte):
        - Specifies the byte order (e.g., little-endian).
    - **`WordOrder`** (1 byte):
        - Specifies the word order.
    - **`FormatLevel`** (1 byte):
        - Indicates the format level.
    - **`CPUType`** (1 byte):
        - Specifies the target CPU (e.g., i386).
    - **`OSType`** (1 byte):
        - Specifies the target operating system (e.g., OS/2).
    - **`ModuleType`** (1 byte):
        - Identifies whether the file is an executable, dynamic library, or driver.
    - **`NumberOfPages`** (4 bytes):
        - Total number of memory pages in the file.
    - **`InitialEIP`** (4 bytes):
        - Initial value of the instruction pointer.
    - **`InitialESP`** (4 bytes):
        - Initial value of the stack pointer.
    - **`PageTableOffset`** (4 bytes):
        - Offset of the page table.
    - **`FixupSectionOffset`** (4 bytes):
        - Offset of the fixup section.
    - **`DataPagesOffset`** (4 bytes):
        - Offset to the data pages.
    - **`ResourceTableOffset`** (4 bytes):
        - Offset of the resource table.

---

## Sections in an LX File

An LX file typically contains:

1. **LX Header**:
    - Contains metadata and loading instructions.

2. **Page Table**:
    - Describes the memory pages, their sizes, and offsets.

3. **Fixup Section**:
    - Provides relocation information to adjust addresses during loading.

4. **Resource Table**:
    - Contains resources such as icons, strings, and bitmaps.

5. **Executable Code**:
    - The actual code and data for the program.

---

## Finding Where the Code Begins

To determine where the code starts in an LX file:

1. **Locate the Entry Point**:
    - The entry point is specified by the `InitialEIP` field in the header.

2. **Calculate the Code Offset**:
    - Combine the `InitialEIP` value with the appropriate page table entry to find the file offset of the code.

3. **Resolve Fixups**:
    - Use the fixup section to adjust addresses as needed.

4. **Disassemble the Code**:
    - Use tools like `objdump` or specialized LX viewers to examine the instructions.

---

## Commands to Analyze LX Files

- **`objdump -f <file>`**:
  Displays the file header and architecture details.

- **`objdump -h <file>`**:
  Displays segment and section headers.

- **`objdump -d <file>`**:
  Disassembles the executable code.

- **`nm <file>`**:
  Lists symbols (if available).

- **LX-specific tools**:
  Use dedicated LX format viewers for detailed analysis.

---

## Example

```bash
# Display header information
objdump -f example.lx

# Display section headers
objdump -h example.lx

# Disassemble to find the entry point
objdump -d example.lx

# Analyze fixups and resources
lxview example.lx
```

These tools can help you analyze the LX structure and understand how the binary is organized and executed.

