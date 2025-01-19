# PEF (Preferred Executable Format)

PEF is the Preferred Executable Format, used primarily on classic Mac OS (System 7.1 and later) for PowerPC applications. It provides a modular and efficient structure for executables, supporting dynamic linking and other advanced features. Here's a breakdown of what the PEF header contains and how you can find where the code begins:

---

## Structure of the PEF Header

The PEF header typically contains the following fields:

1. **Magic Number**:
    - The first four bytes of the file are `Joy!` (0x4A 0x6F 0x79 0x21), which identifies the file as a PEF executable.

2. **Header Fields**:
    - **`Architecture`** (4 bytes):
        - Specifies the target CPU architecture (e.g., PowerPC).
    - **`SectionCount`** (2 bytes):
        - Number of sections in the executable.
    - **`EntryPointSection`** (2 bytes):
        - Index of the section containing the entry point.
    - **`EntryPointOffset`** (4 bytes):
        - Offset within the entry point section where execution begins.
    - **`CodeSectionOffset`** (4 bytes):
        - Offset to the first code section.
    - **`DataSectionOffset`** (4 bytes):
        - Offset to the first data section.
    - **`LoaderInfoOffset`** (4 bytes):
        - Offset to the loader information.
    - **`RelocationInfoOffset`** (4 bytes):
        - Offset to the relocation information.

---

## Sections in a PEF File

A PEF file typically contains:

1. **PEF Header**:
    - Contains metadata and information for loading and linking.

2. **Code Sections**:
    - Contain executable code for the application.

3. **Data Sections**:
    - Contain initialized and uninitialized data.

4. **Loader Information**:
    - Provides details for resolving imported symbols and dynamic linking.

5. **Relocation Information**:
    - Used to adjust addresses during loading.

6. **Resource Information**:
    - Contains application-specific resources like icons, strings, or menus.

---

## Finding Where the Code Begins

To determine where the code starts in a PEF file:

1. **Locate the Entry Point**:
    - The entry point is specified by the `EntryPointSection` and `EntryPointOffset` fields in the header.

2. **Calculate the Code Offset**:
    - Use the section table to find the base offset of the `EntryPointSection`, then add the `EntryPointOffset` to locate the code.

3. **Resolve Relocations**:
    - Use the relocation information to adjust addresses as needed.

4. **Disassemble the Code**:
    - Use tools like `otool` or specialized PEF viewers to examine the instructions.

---

## Commands to Analyze PEF Files

- **`otool -vh <file>`**:
  Displays the file header and architecture details.

- **`otool -l <file>`**:
  Displays section headers and loader information.

- **`otool -tV <file>`**:
  Disassembles the executable code.

- **`nm <file>`**:
  Lists symbols (if available).

- **PEF-specific tools**:
  Use dedicated PEF format viewers for detailed analysis.

---

## Example

```bash
# Display header information
otool -vh example.pef

# Display section headers
otool -l example.pef

# Disassemble to find the entry point
otool -tV example.pef

# Analyze relocation and loader information
pefview example.pef
```

These tools can help you analyze the PEF structure and understand how the binary is organized and executed.

