# Arm64 Syscall calling conventions

The Arm64 calling convention for system calls (syscalls) is a set of rules that dictate how parameters are passed to the kernel, how the syscall number is specified, and how the return value is handled. This ensures that user-space applications can make system calls to the kernel in a standardized way.

## Key Points of the Arm64 Syscall Convention

1. **Registers**:
    - **x0 to x7**: Used to pass up to eight arguments to the syscall.
    - **x8**: Used to specify the syscall number.
    - **x0**: Used to return the result of the syscall.

2. **Syscall Number**:
    - The syscall number is placed in register `x8`.

3. **Parameter Passing**:
    - The first eight arguments are passed in registers `x0` to `x7`.
    - If more than eight arguments are needed, additional arguments are passed on the stack (though this is rare).

4. **Return Value**:
    - The return value of the syscall is placed in register `x0`.
    - If the syscall fails, `x0` contains a negative error code.

5. **Invoking the Syscall**:
    - The `svc #0` instruction is used to invoke the syscall.

## Example

Here is an example of an Arm64 assembly code that makes a syscall to write a string to the standard output (file descriptor 1):

```nasm
.global _start

.section .data
msg:    .asciz "Hello, World!\n"

.section .text
_start:
    // Syscall number for write (64)
    mov x8, #64

    // File descriptor (1 for stdout)
    mov x0, #1

    // Pointer to the message
    ldr x1, =msg

    // Length of the message
    mov x2, #14

    // Invoke the syscall
    svc #0

    // Exit the program
    mov x8, #93    // Syscall number for exit (93)
    mov x0, #0     // Exit code 0
    svc #0
```

## Explanation

- **Data Section**:
    - `msg`: Defines a null-terminated string "Hello, World!\n".

- **Text Section**:
    - `_start`: Entry point of the program.
    - `mov x8, #64`: Sets the syscall number for `write` (64) in `x8`.
    - `mov x0, #1`: Sets the file descriptor (1 for stdout) in `x0`.
    - `ldr x1, =msg`: Loads the address of the message into `x1`.
    - `mov x2, #14`: Sets the length of the message (14 bytes) in `x2`.
    - `svc #0`: Invokes the syscall.
    - `mov x8, #93`: Sets the syscall number for `exit` (93) in `x8`.
    - `mov x0, #0`: Sets the exit code (0) in `x0`.
    - `svc #0`: Invokes the syscall to exit the program.

This example demonstrates how to use the Arm64 syscall convention to perform a simple write operation and then exit the program.