# Hello, World

The "Hello, World!" example provided in this document comes in five different versions to accommodate various architectures and operating systems. Each version is tailored to the specific requirements and system calls of the target environment. The versions include:

1. **AArch64 Assembly for macOS**: This version uses the AArch64 architecture and macOS-specific system calls.
2. **AArch64 Assembly for Linux**: This version is designed for the AArch64 architecture on Linux, utilizing Linux system calls.
3. **x86 Assembly for Linux**: This version targets the x86 architecture on Linux, using the appropriate system calls for this environment.
4. **x86-64 Assembly for Linux**: This version is for the x86-64 architecture on Linux, with system calls suited for 64-bit systems.
5. **x86-64 Assembly for Windows**: This version is written for the x86-64 architecture on Windows, leveraging the Windows API for system calls.

Each version demonstrates how to write and run a simple "Hello, World!" program in assembly language, highlighting the differences in system calls and assembly syntax across various platforms and architectures.

## Hello World Example in AArch64 Assembly for macOS

Here is a simple "Hello, World!" program written in AArch64 assembly for macOS:

```NASM
.section __TEXT,__text,regular,pure_instructions
.globl _start

_start:
    // Write "Hello, World!" to stdout
    mov x0, #1                  // file descriptor (stdout)
    ldr x1, =message            // message to write
    mov x2, #13                 // message length
    mov x16, #4                 // syscall number (sys_write)
    svc #0                      // make syscall

    // Exit the program
    mov x0, #0                  // exit code
    mov x16, #1                 // syscall number (sys_exit)
    svc #0                      // make syscall

.section __TEXT,__cstring,cstring_literals
message:
    .asciz "Hello, World!"
```

### Instructions to Run the AArch64 Assembly Program in macOS

1. **Save the Code**: Save the above code in a file named `hello.s`.

2. **Assemble the Code**: Use the `as` assembler to convert the assembly code into an object file. Open a terminal and navigate to the directory containing `hello.s`. Run the following command:

   ```sh
   as -arch arm64 -o hello.o hello.s
   ```

3. **Link the Object File**: Use the `ld` linker to create an executable from the object file:

   ```sh
   ld -o hello hello.o -lSystem -syslibroot `xcrun --sdk macosx --show-sdk-path` -e _start
   ```

4. **Run the Program**: Execute the generated binary:

   ```sh
   ./hello
   ```

   You should see the output:

   ```
   Hello, World!
   ```

### Summary for AArch64 Assembly on macOS

1. Save the code in `hello.s`.
2. Assemble with `as -arch arm64 -o hello.o hello.s`.
3. Link with `ld -o hello hello.o -lSystem -syslibroot \`xcrun --sdk macosx --show-sdk-path\` -e _start`.
4. Run with `./hello`.

---

## Hello World Example in AArch64 Assembly for Linux

Here is a simple "Hello, World!" program written in AArch64 assembly for Linux:

```NASM
.section .data
message:
    .asciz "Hello, World!\n"

.section .text
.globl _start

_start:
    // Write "Hello, World!" to stdout
    mov x0, #1                  // file descriptor (stdout)
    ldr x1, =message            // message to write
    mov x2, #14                 // message length
    mov x8, #64                 // syscall number (sys_write)
    svc #0                      // make syscall

    // Exit the program
    mov x0, #0                  // exit code
    mov x8, #93                 // syscall number (sys_exit)
    svc #0                      // make syscall
```

### Instructions to Run the AArch64 Assembly Program in Linux

1. **Save the Code**: Save the above code in a file named `hello.s`.

2. **Assemble the Code**: Use the `as` assembler to convert the assembly code into an object file. Open a terminal and navigate to the directory containing `hello.s`. Run the following command:

   ```sh
   as -o hello.o hello.s
   ```

3. **Link the Object File**: Use the `ld` linker to create an executable from the object file:

   ```sh
   ld -o hello hello.o
   ```

4. **Run the Program**: Execute the generated binary:

   ```sh
   ./hello
   ```

   You should see the output:

   ```
   Hello, World!
   ```

### Summary for AArch64 Assembly on Linux

1. Save the code in `hello.s`.
2. Assemble with `as -o hello.o hello.s`.
3. Link with `ld -o hello hello.o`.
4. Run with `./hello`.

---

## Hello World Example in x86 Assembly for Linux

Here is a simple "Hello, World!" program written in x86 assembly for Linux:

```NASM
section .data
    message db 'Hello, World!', 0xA  ; the string to print with a newline character
    message_len equ $ - message      ; the length of the string

section .text
    global _start

_start:
    ; Write "Hello, World!" to stdout
    mov eax, 4          ; syscall number for sys_write
    mov ebx, 1          ; file descriptor (stdout)
    mov ecx, message    ; pointer to the message
    mov edx, message_len; length of the message
    int 0x80            ; make syscall

    ; Exit the program
    mov eax, 1          ; syscall number for sys_exit
    xor ebx, ebx        ; exit code 0
    int 0x80            ; make syscall
```

### Instructions to Run the x86 Assembly Program in Linux

1. **Save the Code**: Save the above code in a file named `hello.asm`.

2. **Assemble the Code**: Use the `nasm` assembler to convert the assembly code into an object file. Open a terminal and navigate to the directory containing `hello.asm`. Run the following command:

   ```sh
   nasm -f elf32 -o hello.o hello.asm
   ```

3. **Link the Object File**: Use the `ld` linker to create an executable from the object file:

   ```sh
   ld -m elf_i386 -o hello hello.o
   ```

4. **Run the Program**: Execute the generated binary:

   ```sh
   ./hello
   ```

   You should see the output:

   ```
   Hello, World!
   ```

### Summary for x86 Assembly on Linux

1. Save the code in `hello.asm`.
2. Assemble with `nasm -f elf32 -o hello.o hello.asm`.
3. Link with `ld -m elf_i386 -o hello hello.o`.
4. Run with `./hello`.

---

## Hello World Example in x86-64 Assembly for Linux

Here is a simple "Hello, World!" program written in x86-64 assembly for Linux:

```NASM
section .data
    message db 'Hello, World!', 0xA  ; the string to print with a newline character
    message_len equ $ - message      ; the length of the string

section .text
    global _start

_start:
    ; Write "Hello, World!" to stdout
    mov rax, 1          ; syscall number for sys_write
    mov rdi, 1          ; file descriptor (stdout)
    mov rsi, message    ; pointer to the message
    mov rdx, message_len; length of the message
    syscall             ; make syscall

    ; Exit the program
    mov rax, 60         ; syscall number for sys_exit
    xor rdi, rdi        ; exit code 0
    syscall             ; make syscall
```

### Instructions to Run the x86-64 Assembly Program in Linux

1. **Save the Code**: Save the above code in a file named `hello.asm`.

2. **Assemble the Code**: Use the `nasm` assembler to convert the assembly code into an object file. Open a terminal and navigate to the directory containing `hello.asm`. Run the following command:

   ```sh
   nasm -f elf64 -o hello.o hello.asm
   ```

3. **Link the Object File**: Use the `ld` linker to create an executable from the object file:

   ```sh
   ld -o hello hello.o
   ```

4. **Run the Program**: Execute the generated binary:

   ```sh
   ./hello
   ```

   You should see the output:

   ```
   Hello, World!
   ```

### Summary for x86-64 Assembly on Linux

1. Save the code in `hello.asm`.
2. Assemble with `nasm -f elf64 -o hello.o hello.asm`.
3. Link with `ld -o hello hello.o`.
4. Run with `./hello`.


---

## Hello World Example in x86-64 Assembly for Windows

Here is a simple "Hello, World!" program written in x86-64 assembly for Windows using the Windows API:

```NASM
section .data
    message db 'Hello, World!', 0  ; the string to print with a null terminator
    message_len equ $ - message    ; the length of the string

section .text
    extern  GetStdHandle
    extern  WriteConsoleA
    extern  ExitProcess
    global  main

main:
    ; Get handle to stdout
    sub     rsp, 28h               ; allocate shadow space
    mov     ecx, -11               ; STD_OUTPUT_HANDLE
    call    GetStdHandle
    mov     rcx, rax               ; handle to stdout

    ; Write "Hello, World!" to stdout
    lea     rdx, [message]         ; pointer to the message
    mov     r8d, message_len       ; length of the message
    lea     r9, [rsp+20h]          ; pointer to the number of characters written
    mov     qword [rsp+20h], 0     ; initialize number of characters written to 0
    call    WriteConsoleA

    ; Exit the program
    xor     ecx, ecx               ; exit code 0
    call    ExitProcess
```

### Instructions to Run the x86-64 Assembly Program in Windows

1. **Save the Code**: Save the above code in a file named `hello.asm`.

2. **Assemble the Code**: Use the `nasm` assembler to convert the assembly code into an object file. Open a terminal and navigate to the directory containing `hello.asm`. Run the following command:

   ```sh
   nasm -f win64 -o hello.obj hello.asm
   ```

3. **Link the Object File**: Use a linker like `GoLink` to create an executable from the object file:

   ```sh
   golink /entry main /console hello.obj kernel32.dll
   ```

4. **Run the Program**: Execute the generated binary:

   ```sh
   hello.exe
   ```

   You should see the output:

   ```
   Hello, World!
   ```

### Summary for x86-64 Assembly on Windows

1. Save the code in `hello.asm`.
2. Assemble with `nasm -f win64 -o hello.obj hello.asm`.
3. Link with `golink /entry main /console hello.obj kernel32.dll`.
4. Run with `hello.exe`.