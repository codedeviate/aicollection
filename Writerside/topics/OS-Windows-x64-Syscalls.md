# x64 Syscalls

## Common Windows 11 Syscalls

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
    section .bss
    buffer resb 100

    section .data
    io_status resb 16

    section .text
    global _start

    _start:
        mov r10, rcx        ; Syscall number for NtReadFile
        mov eax, 0x00000003
        mov rcx, 0x4        ; File handle (example)
        lea rdx, [io_status]; Pointer to IO status block
        lea r8, [buffer]    ; Pointer to the buffer
        mov r9, 100         ; Number of bytes to read
        mov rax, 0          ; Byte offset (example)
        syscall             ; Invoke the syscall

        mov r10, rcx        ; Syscall number for NtTerminateProcess
        mov eax, 0x0000002C
        xor ecx, ecx        ; Process handle (current process)
        xor edx, edx        ; Exit status
        syscall             ; Invoke the syscall
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
    section .data
    msg db "Hello, World!", 0xA
    io_status resb 16

    section .text
    global _start

    _start:
        mov r10, rcx        ; Syscall number for NtWriteFile
        mov eax, 0x00000004
        mov rcx, 0x4        ; File handle (example)
        lea rdx, [io_status]; Pointer to IO status block
        lea r8, [msg]       ; Pointer to the message
        mov r9, 14          ; Length of the message
        mov rax, 0          ; Byte offset (example)
        syscall             ; Invoke the syscall

        mov r10, rcx        ; Syscall number for NtTerminateProcess
        mov eax, 0x0000002C
        xor ecx, ecx        ; Process handle (current process)
        xor edx, edx        ; Exit status
        syscall             ; Invoke the syscall
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
    section .data
    path db "\\??\\C:\\path\\to\\file", 0
    file_handle resq 1
    io_status resb 16
    obj_attr resb 24

    section .text
    global _start

    _start:
        mov r10, rcx        ; Syscall number for NtOpenFile
        mov eax, 0x00000005
        lea rcx, [file_handle]; Pointer to file handle
        mov rdx, 0x120089   ; Desired access (example)
        lea r8, [obj_attr]  ; Pointer to object attributes
        lea r9, [io_status] ; Pointer to IO status block
        mov rax, 0x7        ; Share access (example)
        mov rbx, 0x20       ; Open options (example)
        syscall             ; Invoke the syscall

        mov r10, rcx        ; Syscall number for NtTerminateProcess
        mov eax, 0x0000002C
        xor ecx, ecx        ; Process handle (current process)
        xor edx, edx        ; Exit status
        syscall             ; Invoke the syscall
    ```

4. **`NtClose`** (syscall number 0x0000000C)
    - **Description**: Closes a handle.
    - **Arguments**:
        - `HANDLE Handle`: Handle to close.
    - **Return Value**: NTSTATUS code.

    ```nasm
    section .text
    global _start

    _start:
        mov r10, rcx        ; Syscall number for NtClose
        mov eax, 0x0000000C
        mov rcx, 0x4        ; Handle (example)
        syscall             ; Invoke the syscall

        mov r10, rcx        ; Syscall number for NtTerminateProcess
        mov eax, 0x0000002C
        xor ecx, ecx        ; Process handle (current process)
        xor edx, edx        ; Exit status
        syscall             ; Invoke the syscall
    ```

5. **`NtTerminateProcess`** (syscall number 0x0000002C)
    - **Description**: Terminates a process.
    - **Arguments**:
        - `HANDLE ProcessHandle`: Handle to the process.
        - `NTSTATUS ExitStatus`: Exit status.
    - **Return Value**: NTSTATUS code.

    ```nasm
    section .text
    global _start

    _start:
        mov r10, rcx        ; Syscall number for NtTerminateProcess
        mov eax, 0x0000002C
        xor ecx, ecx        ; Process handle (current process)
        xor edx, edx        ; Exit status
        syscall             ; Invoke the syscall
    ```

These examples demonstrate how to use the Windows 11 syscall convention on x64 to perform basic operations such as reading, writing, opening, closing files, and terminating a process. For a complete list of syscalls, refer to the Windows kernel documentation.