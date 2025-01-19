# LE (Linear Executable Format)

LE is the Linear Executable format, primarily used in OS/2 and some early Windows environments for device drivers and virtual device drivers (VxDs). It supports 32-bit addressing and demand-paging, making it a significant evolution over earlier formats like MZ. Here's a breakdown of what the LE header contains and how you can find where the code begins:

---

## Structure of the LE Header

The LE header typically contains the following fields:

1. **Magic Number**:
    - The first four bytes of the file are `LE` (0x4C 0x45), which identifies the file as a Linear Executable.

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
        - Specifies the target operating system (e.g., OS/2 or Windows).
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

## Sections in an LE File

An LE file typically contains:

1. **LE Header**:
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

To determine where the code starts in an LE file:

1. **Locate the Entry Point**:
    - The entry point is specified by the `InitialEIP` field in the header.

2. **Calculate the Code Offset**:
    - Combine the `InitialEIP` value with the appropriate page table entry to find the file offset of the code.

3. **Resolve Fixups**:
    - Use the fixup section to adjust addresses as needed.

4. **Disassemble the Code**:
    - Use tools like `objdump` or specialized LE viewers to examine the instructions.

---

## Commands to Analyze LE Files

- **`objdump -f <file>`**:
  Displays the file header and architecture details.

- **`objdump -h <file>`**:
  Displays segment and section headers.

- **`objdump -d <file>`**:
  Disassembles the executable code.

- **`nm <file>`**:
  Lists symbols (if available).

- **LE-specific tools**:
  Use dedicated LE format viewers for detailed analysis.

---

## Example

```bash
# Display header information
objdump -f example.le

# Display section headers
objdump -h example.le

# Disassemble to find the entry point
objdump -d example.le

# Analyze fixups and resources
leview example.le
```

These tools can help you analyze the LE structure and understand how the binary is organized and executed.

