# MZ (DOS Executable Format)

MZ is the original executable file format used in DOS. Named after Mark Zbikowski, the format defines the structure of DOS `.exe` files and provides basic information for the DOS operating system to load and execute the program. Here's a breakdown of what the MZ header contains and how you can find where the code begins:

---

## Structure of the MZ Header

The MZ header typically contains the following fields:

1. **Magic Number**:
    - The first two bytes of the file are `MZ` (0x4D 0x5A), which identifies the file as an MZ executable.

2. **Header Fields**:
    - **`BytesOnLastPage`** (2 bytes):
        - Number of bytes used on the last page of the file.
    - **`PagesInFile`** (2 bytes):
        - Total number of 512-byte pages in the file.
    - **`RelocationEntries`** (2 bytes):
        - Number of entries in the relocation table.
    - **`HeaderParagraphs`** (2 bytes):
        - Size of the header in 16-byte paragraphs.
    - **`MinExtraParagraphs`** (2 bytes):
        - Minimum additional memory needed to run the program.
    - **`MaxExtraParagraphs`** (2 bytes):
        - Maximum additional memory the program can use.
    - **`InitialSS`** (2 bytes):
        - Initial value of the stack segment register.
    - **`InitialSP`** (2 bytes):
        - Initial value of the stack pointer.
    - **`Checksum`** (2 bytes):
        - File checksum (often unused).
    - **`InitialIP`** (2 bytes):
        - Initial value of the instruction pointer.
    - **`InitialCS`** (2 bytes):
        - Initial value of the code segment register.
    - **`RelocationTableOffset`** (2 bytes):
        - Offset of the relocation table.
    - **`OverlayNumber`** (2 bytes):
        - Overlay number (0 for main program).

---

## Sections in an MZ File

An MZ file typically contains:

1. **MZ Header**:
    - Contains metadata and loading instructions for DOS.

2. **Relocation Table**:
    - Used to adjust segment-based addresses during program loading.

3. **Executable Code**:
    - The actual code and data for the program.

4. **Optional Data**:
    - Additional data such as debugging information or overlays.

---

## Finding Where the Code Begins

To determine where the code starts in an MZ file:

1. **Locate the Code Segment**:
    - The code segment is specified by the `InitialCS` field in the header.

2. **Calculate the Code Offset**:
    - Combine the `InitialCS` value (shifted left by 4 bits) with the start of the executable section.
    - Example:
      ```
      code_offset = (InitialCS << 4) + HeaderSize
      ```

3. **Disassemble the Code**:
    - Use tools like `debug` or `objdump` to examine the instructions.

---

## Commands to Analyze MZ Files

- **`objdump -f <file>`**:
  Displays the file header and architecture details.

- **`objdump -h <file>`**:
  Displays segment and section headers.

- **`objdump -d <file>`**:
  Disassembles the executable code.

- **`nm <file>`**:
  Lists symbols (if available).

- **`debug <file>`** (on DOS systems):
  Allows interactive inspection of the MZ binary.

---

## Example

```bash
# Display header information
objdump -f example.exe

# Display segment headers
objdump -h example.exe

# Disassemble to find the entry point
objdump -d example.exe

# Use DOS debug
debug example.exe
```

These tools can help you analyze the MZ structure and understand how the binary is organized and executed.

