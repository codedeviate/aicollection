# Arm64 Syscalls

## Common macOS Syscalls

1. **`read`** (syscall number 3)
    - **Description**: Reads data from a file descriptor.
    - **Arguments**:
        - `x0`: File descriptor.
        - `x1`: Buffer to store the read data.
        - `x2`: Number of bytes to read.
    - **Return Value**: Number of bytes read or a negative error code.

    ```nasm
    .global _start

    .section .bss
    buffer: .skip 100

    .section .text
    _start:
        mov x16, #3        // Syscall number for read
        mov x0, #0         // File descriptor (stdin)
        ldr x1, =buffer    // Pointer to the buffer
        mov x2, #100       // Number of bytes to read
        svc #0             // Invoke the syscall

        mov x16, #1        // Syscall number for exit
        mov x0, #0         // Exit code 0
        svc #0             // Invoke the syscall
    ```

2. **`write`** (syscall number 4)
    - **Description**: Writes data to a file descriptor.
    - **Arguments**:
        - `x0`: File descriptor.
        - `x1`: Buffer containing the data to write.
        - `x2`: Number of bytes to write.
    - **Return Value**: Number of bytes written or a negative error code.

    ```nasm
    .global _start

    .section .data
    msg:    .asciz "Hello, World!\n"

    .section .text
    _start:
        mov x16, #4        // Syscall number for write
        mov x0, #1         // File descriptor (stdout)
        ldr x1, =msg       // Pointer to the message
        mov x2, #14        // Length of the message
        svc #0             // Invoke the syscall

        mov x16, #1        // Syscall number for exit
        mov x0, #0         // Exit code 0
        svc #0             // Invoke the syscall
    ```

3. **`open`** (syscall number 5)
    - **Description**: Opens a file.
    - **Arguments**:
        - `x0`: Path to the file.
        - `x1`: Flags.
        - `x2`: Mode (optional, used when creating a file).
    - **Return Value**: File descriptor or a negative error code.

    ```nasm
    .global _start

    .section .data
    path:   .asciz "/path/to/file"

    .section .text
    _start:
        mov x16, #5        // Syscall number for open
        ldr x0, =path      // Path to the file
        mov x1, #0         // Flags (O_RDONLY)
        mov x2, #0         // Mode (not used)
        svc #0             // Invoke the syscall

        mov x16, #1        // Syscall number for exit
        mov x0, #0         // Exit code 0
        svc #0             // Invoke the syscall
    ```

4. **`close`** (syscall number 6)
    - **Description**: Closes a file descriptor.
    - **Arguments**:
        - `x0`: File descriptor.
    - **Return Value**: 0 on success or a negative error code.

    ```nasm
    .global _start

    .section .text
    _start:
        mov x16, #6        // Syscall number for close
        mov x0, #3         // File descriptor
        svc #0             // Invoke the syscall

        mov x16, #1        // Syscall number for exit
        mov x0, #0         // Exit code 0
        svc #0             // Invoke the syscall
    ```

5. **`exit`** (syscall number 1)
    - **Description**: Terminates the calling process.
    - **Arguments**:
        - `x0`: Exit status.
    - **Return Value**: Does not return.

    ```nasm
    .global _start

    .section .text
    _start:
        mov x16, #1        // Syscall number for exit
        mov x0, #0         // Exit code 0
        svc #0             // Invoke the syscall
    ```

These examples demonstrate how to use the macOS syscall convention on Arm64 to perform basic operations such as reading, writing, opening, closing files, and exiting a program. For a complete list of syscalls, refer to the macOS kernel documentation.