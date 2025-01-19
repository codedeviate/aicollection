# PE (Portable Executable)

The PE (Portable Executable) format is the standard file format for executables, object code, DLLs, and other binaries on Windows systems. It is derived from the COFF (Common Object File Format) and is used by the Windows operating system for loading and running programs. Here's a breakdown of what the PE header contains and how you can find where the code begins:

---

## Structure of the PE Header

The PE header typically contains the following fields:

1. **DOS Header**:
    - Begins with the magic number `MZ` (Mark Zbikowski).
    - Contains a pointer to the PE header (`e_lfanew`).

2. **PE Signature**:
    - The string `PE\0\0` (4 bytes).

3. **COFF File Header**:
    - **`Machine` (2 bytes)**:
        - Specifies the target architecture (e.g., `IMAGE_FILE_MACHINE_I386` for x86, `IMAGE_FILE_MACHINE_AMD64` for x64).
    - **`NumberOfSections` (2 bytes)**:
        - Number of sections in the binary.
    - **`TimeDateStamp` (4 bytes)**:
        - Timestamp of when the binary was created.
    - **`PointerToSymbolTable` (4 bytes)**:
        - Offset to the symbol table (deprecated in modern PE files).
    - **`NumberOfSymbols` (4 bytes)**:
        - Number of symbols (deprecated).
    - **`SizeOfOptionalHeader` (2 bytes)**:
        - Size of the optional header.
    - **`Characteristics` (2 bytes)**:
        - Flags describing the attributes of the binary (e.g., executable, DLL, etc.).

4. **Optional Header**:
    - Contains information about the binary's layout in memory.
    - Divided into:
        - **Standard fields**: Entry point, image base, section alignment.
        - **Windows-specific fields**: DLL characteristics, stack/heap size, subsystem type.
        - **Data directories**: Pointers to tables like import/export tables and resources.

---

## Sections in a PE File

Following the headers are sections, each describing a part of the binary:

1. **`.text`**:
    - Contains executable code.

2. **`.data`**:
    - Contains initialized data.

3. **`.bss`**:
    - Contains uninitialized data.

4. **`.rdata`**:
    - Contains read-only data (e.g., constants, import/export tables).

5. **`.rsrc`**:
    - Contains resources (e.g., icons, menus).

6. **`.reloc`**:
    - Contains relocation information for dynamic linking.

---

## Finding Where the Code Begins

To determine where the code starts, follow these steps:

1. **Locate the Entry Point**:
    - The entry point is specified in the Optional Header's `AddressOfEntryPoint` field.
    - This is a relative virtual address (RVA) and needs to be converted to a file offset.

2. **Convert RVA to File Offset**:
    - Use the section headers to map the RVA to a file offset:
      ```
      file_offset = RVA - VirtualAddress + PointerToRawData
      ```

3. **Verify with Disassembly**:
    - Use tools like `dumpbin`, `objdump`, or IDA Pro to disassemble and confirm the entry point.

---

## Commands to Analyze PE Headers

- **`dumpbin /headers <file>`**:
  Displays the PE headers and sections.

- **`dumpbin /disasm <file>`**:
  Disassembles the binary.

- **`objdump -p <file>`**:
  Displays the PE headers and import/export tables (if GNU Binutils is available).

- **`pedump <file>`**:
  A dedicated tool for dumping PE headers.

---

## Example

```bash
# Display PE headers using dumpbin
dumpbin /headers example.exe

# Disassemble to find the entry point
dumpbin /disasm example.exe
```

These tools can help you analyze the PE structure and understand how the binary is organized and executed.

