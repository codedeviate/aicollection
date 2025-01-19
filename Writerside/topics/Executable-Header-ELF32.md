# ELF32

The ELF (Executable and Linkable Format) header of an `elf32` executable contains metadata about the file, including essential information that helps the operating system or loader interpret and execute the binary. Here's a breakdown of what the ELF header contains and how you can find where the code begins:

---

## Structure of the ELF32 Header
The ELF32 header typically contains the following fields:

1. **`e_ident` (16 bytes)**:
    - Magic number (`0x7f 'E' 'L' 'F'`).
    - File class (32-bit or 64-bit).
    - Data encoding (little-endian or big-endian).
    - ELF version.
    - OS/ABI information.
    - Padding for alignment.

2. **`e_type` (2 bytes)**:
    - Type of file (e.g., `ET_EXEC` for executable, `ET_DYN` for shared object, etc.).

3. **`e_machine` (2 bytes)**:
    - Target architecture (e.g., `EM_386` for x86).

4. **`e_version` (4 bytes)**:
    - ELF version (usually 1).

5. **`e_entry` (4 bytes)**:
    - The virtual address of the entry point where execution starts (beginning of the code).

6. **`e_phoff` (4 bytes)**:
    - Offset of the program header table (for runtime execution).

7. **`e_shoff` (4 bytes)**:
    - Offset of the section header table (for debugging and linking).

8. **`e_flags` (4 bytes)**:
    - Architecture-specific flags.

9. **`e_ehsize` (2 bytes)**:
    - Size of the ELF header.

10. **`e_phentsize` (2 bytes)**:
    - Size of each program header table entry.

11. **`e_phnum` (2 bytes)**:
    - Number of entries in the program header table.

12. **`e_shentsize` (2 bytes)**:
    - Size of each section header table entry.

13. **`e_shnum` (2 bytes)**:
    - Number of entries in the section header table.

14. **`e_shstrndx` (2 bytes)**:
    - Index of the section header string table.

---

## Finding Where the Code Begins
To determine where the code starts, follow these steps:

1. **Check the Entry Point (`e_entry`)**:
    - The `e_entry` field in the ELF header gives the virtual address of the entry point where execution begins. However, this is a virtual address, so you may need to map it to a file offset.

2. **Locate the Program Header (`e_phoff`)**:
    - The program header table describes memory segments of the executable, including the code segment (`PT_LOAD`).

3. **Find the Code Segment**:
    - Look for a segment in the program header with the type `PT_LOAD` and executable permission flags (`PF_X`).
    - This segment's `p_offset` field gives the file offset of the segment.
    - The `p_vaddr` field provides the virtual address of the segment.

4. **Map Entry Point to File Offset**:
    - Use the `e_entry` virtual address and compare it with the `p_vaddr` of the segment containing the code. The corresponding offset within the file can be calculated as:
      ```
      file_offset = e_entry - p_vaddr + p_offset
      ```

5. **Verify with Disassembly**:
    - Use tools like `objdump` or `readelf` to disassemble the binary and verify the entry point.

---

## Commands to Analyze ELF Headers
- **`readelf -h <file>`**:
  Displays the ELF header, including `e_entry`, `e_phoff`, and more.

- **`readelf -l <file>`**:
  Displays the program headers and segments, including their file offsets and virtual addresses.

- **`objdump -d <file>`**:
  Disassembles the executable, allowing you to examine the code.

---

## Example
```bash
# Display ELF header
readelf -h example

# Display program headers
readelf -l example

# Disassemble to find the entry point
objdump -d example
```

These tools can help you locate the exact location of the code and understand the structure of the ELF executable.

