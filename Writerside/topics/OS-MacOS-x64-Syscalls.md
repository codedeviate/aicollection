# x64 Syscalls

## Common macOS Syscalls

1. **`read`** (syscall number 0x2000003)
    - **Description**: Reads data from a file descriptor.
    - **Arguments**:
        - `rdi`: File descriptor.
        - `rsi`: Buffer to store the read data.
        - `rdx`: Number of bytes to read.
    - **Return Value**: Number of bytes read or a negative error code.

    ```nasm
    section .bss
    buffer resb 100

    section .text
    global _start

    _start:
        mov rax, 0x2000003  ; Syscall number for read
        mov rdi, 0          ; File descriptor (stdin)
        lea rsi, [buffer]   ; Pointer to the buffer
        mov rdx, 100        ; Number of bytes to read
        syscall             ; Invoke the syscall

        mov rax, 0x2000001  ; Syscall number for exit
        xor rdi, rdi        ; Exit code 0
        syscall             ; Invoke the syscall
    ```

2. **`write`** (syscall number 0x2000004)
    - **Description**: Writes data to a file descriptor.
    - **Arguments**:
        - `rdi`: File descriptor.
        - `rsi`: Buffer containing the data to write.
        - `rdx`: Number of bytes to write.
    - **Return Value**: Number of bytes written or a negative error code.

    ```nasm
    section .data
    msg db "Hello, World!", 0xA

    section .text
    global _start

    _start:
        mov rax, 0x2000004  ; Syscall number for write
        mov rdi, 1          ; File descriptor (stdout)
        lea rsi, [msg]      ; Pointer to the message
        mov rdx, 14         ; Length of the message
        syscall             ; Invoke the syscall

        mov rax, 0x2000001  ; Syscall number for exit
        xor rdi, rdi        ; Exit code 0
        syscall             ; Invoke the syscall
    ```

3. **`open`** (syscall number 0x2000005)
    - **Description**: Opens a file.
    - **Arguments**:
        - `rdi`: Path to the file.
        - `rsi`: Flags.
        - `rdx`: Mode (optional, used when creating a file).
    - **Return Value**: File descriptor or a negative error code.

    ```nasm
    section .data
    path db "/path/to/file", 0

    section .text
    global _start

    _start:
        mov rax, 0x2000005  ; Syscall number for open
        lea rdi, [path]     ; Path to the file
        xor rsi, rsi        ; Flags (O_RDONLY)
        xor rdx, rdx        ; Mode (not used)
        syscall             ; Invoke the syscall

        mov rax, 0x2000001  ; Syscall number for exit
        xor rdi, rdi        ; Exit code 0
        syscall             ; Invoke the syscall
    ```

4. **`close`** (syscall number 0x2000006)
    - **Description**: Closes a file descriptor.
    - **Arguments**:
        - `rdi`: File descriptor.
    - **Return Value**: 0 on success or a negative error code.

    ```nasm
    section .text
    global _start

    _start:
        mov rax, 0x2000006  ; Syscall number for close
        mov rdi, 3          ; File descriptor
        syscall             ; Invoke the syscall

        mov rax, 0x2000001  ; Syscall number for exit
        xor rdi, rdi        ; Exit code 0
        syscall             ; Invoke the syscall
    ```

5. **`exit`** (syscall number 0x2000001)
    - **Description**: Terminates the calling process.
    - **Arguments**:
        - `rdi`: Exit status.
    - **Return Value**: Does not return.

    ```nasm
    section .text
    global _start

    _start:
        mov rax, 0x2000001  ; Syscall number for exit
        xor rdi, rdi        ; Exit code 0
        syscall             ; Invoke the syscall
    ```

These examples demonstrate how to use the macOS syscall convention on x64 to perform basic operations such as reading, writing, opening, closing files, and exiting a program. For a complete list of syscalls, refer to the macOS kernel documentation.