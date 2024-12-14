# Arm64 Syscalls

Listing all Arm64 syscalls in-depth is extensive, but I can provide an overview of some common syscalls along with examples. For a complete list, you can refer to the Linux kernel source or documentation.

## Common Arm64 Syscalls

1. **`read`** (syscall number 63)
    - **Description**: Reads data from a file descriptor.
    - **Arguments**:
        - `x0`: File descriptor.
        - `x1`: Buffer to store the read data.
        - `x2`: Number of bytes to read.
    - **Return Value**: Number of bytes read or a negative error code.

2. **`write`** (syscall number 64)
    - **Description**: Writes data to a file descriptor.
    - **Arguments**:
        - `x0`: File descriptor.
        - `x1`: Buffer containing the data to write.
        - `x2`: Number of bytes to write.
    - **Return Value**: Number of bytes written or a negative error code.

3. **`open`** (syscall number 56)
    - **Description**: Opens a file.
    - **Arguments**:
        - `x0`: Path to the file.
        - `x1`: Flags.
        - `x2`: Mode (optional, used when creating a file).
    - **Return Value**: File descriptor or a negative error code.

4. **`close`** (syscall number 57)
    - **Description**: Closes a file descriptor.
    - **Arguments**:
        - `x0`: File descriptor.
    - **Return Value**: 0 on success or a negative error code.

5. **`exit`** (syscall number 93)
    - **Description**: Terminates the calling process.
    - **Arguments**:
        - `x0`: Exit status.
    - **Return Value**: Does not return.

## Examples

### `write` syscall example

```nasm
.global _start

.section .data
msg:    .asciz "Hello, World!\n"

.section .text
_start:
    mov x8, #64        // Syscall number for write
    mov x0, #1         // File descriptor (stdout)
    ldr x1, =msg       // Pointer to the message
    mov x2, #14        // Length of the message
    svc #0             // Invoke the syscall

    mov x8, #93        // Syscall number for exit
    mov x0, #0         // Exit code 0
    svc #0             // Invoke the syscall
```

### `read` syscall example

```nasm
.global _start

.section .bss
buffer: .skip 100

.section .text
_start:
    mov x8, #63        // Syscall number for read
    mov x0, #0         // File descriptor (stdin)
    ldr x1, =buffer    // Pointer to the buffer
    mov x2, #100       // Number of bytes to read
    svc #0             // Invoke the syscall

    mov x8, #64        // Syscall number for write
    mov x0, #1         // File descriptor (stdout)
    ldr x1, =buffer    // Pointer to the buffer
    mov x2, #100       // Number of bytes to write
    svc #0             // Invoke the syscall

    mov x8, #93        // Syscall number for exit
    mov x0, #0         // Exit code 0
    svc #0             // Invoke the syscall
```

These examples demonstrate how to use the Arm64 syscall convention to perform basic read and write operations. For a complete list of syscalls, refer to the Linux kernel documentation.