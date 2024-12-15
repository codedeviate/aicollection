# Arm64 Syscalls

### Common Windows 11 Syscalls

1. **`NtReadFile`** (syscall number 0x00000003)
    - **Description**: Reads data from a file.
    - **Arguments**:
        - `HANDLE FileHandle`: Handle to the file.
        - `PIO_STATUS_BLOCK IoStatusBlock`: Pointer to an IO status block.
        - `PVOID Buffer`: Buffer to store the read data.
        - `ULONG Length`: Number of bytes to read.
        - `PLARGE_INTEGER ByteOffset`: Pointer to the byte offset.
    - **Return Value**: NTSTATUS code.

    ```nasm
    .global _start

    .section .bss
    buffer: .skip 100

    .section .text
    _start:
        mov x8, #0x00000003  // Syscall number for NtReadFile
        mov x0, #0x4         // File handle (example)
        ldr x1, =io_status   // Pointer to IO status block
        ldr x2, =buffer      // Pointer to the buffer
        mov x3, #100         // Number of bytes to read
        mov x4, #0           // Byte offset (example)
        svc #0               // Invoke the syscall

        mov x8, #0x0000002C  // Syscall number for NtTerminateProcess
        mov x0, #0           // Process handle (current process)
        mov x1, #0           // Exit status
        svc #0               // Invoke the syscall

    .section .bss
    io_status: .skip 16
    ```

2. **`NtWriteFile`** (syscall number 0x00000004)
    - **Description**: Writes data to a file.
    - **Arguments**:
        - `HANDLE FileHandle`: Handle to the file.
        - `PIO_STATUS_BLOCK IoStatusBlock`: Pointer to an IO status block.
        - `PVOID Buffer`: Buffer containing the data to write.
        - `ULONG Length`: Number of bytes to write.
        - `PLARGE_INTEGER ByteOffset`: Pointer to the byte offset.
    - **Return Value**: NTSTATUS code.

    ```nasm
    .global _start

    .section .data
    msg:    .asciz "Hello, World!\n"

    .section .text
    _start:
        mov x8, #0x00000004  // Syscall number for NtWriteFile
        mov x0, #0x4         // File handle (example)
        ldr x1, =io_status   // Pointer to IO status block
        ldr x2, =msg         // Pointer to the message
        mov x3, #14          // Length of the message
        mov x4, #0           // Byte offset (example)
        svc #0               // Invoke the syscall

        mov x8, #0x0000002C  // Syscall number for NtTerminateProcess
        mov x0, #0           // Process handle (current process)
        mov x1, #0           // Exit status
        svc #0               // Invoke the syscall

    .section .bss
    io_status: .skip 16
    ```

3. **`NtOpenFile`** (syscall number 0x00000005)
    - **Description**: Opens a file.
    - **Arguments**:
        - `PHANDLE FileHandle`: Pointer to a handle to the file.
        - `ACCESS_MASK DesiredAccess`: Desired access.
        - `POBJECT_ATTRIBUTES ObjectAttributes`: Pointer to object attributes.
        - `PIO_STATUS_BLOCK IoStatusBlock`: Pointer to an IO status block.
        - `ULONG ShareAccess`: Share access.
        - `ULONG OpenOptions`: Open options.
    - **Return Value**: NTSTATUS code.

    ```nasm
    .global _start

    .section .data
    path:   .asciz "\\??\\C:\\path\\to\\file"

    .section .text
    _start:
        mov x8, #0x00000005  // Syscall number for NtOpenFile
        ldr x0, =file_handle // Pointer to file handle
        mov x1, #0x120089    // Desired access (example)
        ldr x2, =obj_attr    // Pointer to object attributes
        ldr x3, =io_status   // Pointer to IO status block
        mov x4, #0x7         // Share access (example)
        mov x5, #0x20        // Open options (example)
        svc #0               // Invoke the syscall

        mov x8, #0x0000002C  // Syscall number for NtTerminateProcess
        mov x0, #0           // Process handle (current process)
        mov x1, #0           // Exit status
        svc #0               // Invoke the syscall

    .section .bss
    file_handle: .skip 8
    io_status: .skip 16
    obj_attr: .skip 24
    ```

4. **`NtClose`** (syscall number 0x0000000C)
    - **Description**: Closes a handle.
    - **Arguments**:
        - `HANDLE Handle`: Handle to close.
    - **Return Value**: NTSTATUS code.

    ```nasm
    .global _start

    .section .text
    _start:
        mov x8, #0x0000000C  // Syscall number for NtClose
        mov x0, #0x4         // Handle (example)
        svc #0               // Invoke the syscall

        mov x8, #0x0000002C  // Syscall number for NtTerminateProcess
        mov x0, #0           // Process handle (current process)
        mov x1, #0           // Exit status
        svc #0               // Invoke the syscall
    ```

5. **`NtTerminateProcess`** (syscall number 0x0000002C)
    - **Description**: Terminates a process.
    - **Arguments**:
        - `HANDLE ProcessHandle`: Handle to the process.
        - `NTSTATUS ExitStatus`: Exit status.
    - **Return Value**: NTSTATUS code.

    ```nasm
    .global _start

    .section .text
    _start:
        mov x8, #0x0000002C  // Syscall number for NtTerminateProcess
        mov x0, #0           // Process handle (current process)
        mov x1, #0           // Exit status
        svc #0               // Invoke the syscall
    ```

These examples demonstrate how to use the Windows 11 syscall convention on Arm64 to perform basic operations such as reading, writing, opening, closing files, and terminating a process. For a complete list of syscalls, refer to the Windows kernel documentation.