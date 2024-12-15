# x64 Registers

## General Purpose Registers

1. **RAX (Accumulator Register)**
    - Used for arithmetic operations and as a return value register.
    - Example:
      ```nasm
      mov rax, 5      ; Move 5 into RAX
      add rax, 3      ; Add 3 to RAX, RAX now contains 8
      ```

2. **RBX (Base Register)**
    - Used as a base pointer for memory access.
    - Example:
      ```nasm
      mov rbx, 0x1000 ; Move address 0x1000 into RBX
      mov rax, [rbx]  ; Move the value at address 0x1000 into RAX
      ```

3. **RCX (Counter Register)**
    - Used for loop operations and as the fourth argument in function calls.
    - Example:
      ```nasm
      mov rcx, 10     ; Set loop counter to 10
      loop_start:
      ; Loop body
      loop loop_start ; Decrement RCX and jump to loop_start if RCX is not zero
      ```

4. **RDX (Data Register)**
    - Used for I/O operations, arithmetic operations, and as the third argument in function calls.
    - Example:
      ```nasm
      mov rax, 10
      mov rdx, 2
      mul rdx         ; Multiply RAX by RDX, result in RAX, high-order bits in RDX
      ```

5. **RSI (Source Index)**
    - Used for string and array operations, and as the second argument in function calls.
    - Example:
      ```nasm
      mov rsi, source ; Point RSI to the source array
      mov rdi, dest   ; Point RDI to the destination array
      mov rcx, length ; Set the length of the array
      rep movsb       ; Copy bytes from [RSI] to [RDI], RCX times
      ```

6. **RDI (Destination Index)**
    - Used for string and array operations, and as the first argument in function calls.
    - Example:
      ```nasm
      mov rsi, source ; Point RSI to the source array
      mov rdi, dest   ; Point RDI to the destination array
      mov rcx, length ; Set the length of the array
      rep movsb       ; Copy bytes from [RSI] to [RDI], RCX times
      ```

7. **RBP (Base Pointer)**
    - Used to point to the base of the stack frame.
    - Example:
      ```nasm
      push rbp        ; Save old base pointer
      mov rbp, rsp    ; Set new base pointer
      sub rsp, 16     ; Allocate 16 bytes on the stack
      ```

8. **RSP (Stack Pointer)**
    - Points to the top of the stack.
    - Example:
      ```nasm
      push rax        ; Push RAX onto the stack
      pop rbx         ; Pop the top of the stack into RBX
      ```

9. **R8 - R15 (Extended General Purpose Registers)**
    - Additional registers for general use and function arguments.
    - Example:
      ```nasm
      mov r8, 20      ; Move 20 into R8
      add r8, 10      ; Add 10 to R8, R8 now contains 30
      ```

## Segment Registers

1. **CS (Code Segment)**
    - Points to the segment containing the current program code.
    - Example:
      ```nasm
      mov ax, cs      ; Move the code segment value into AX
      ```

2. **DS (Data Segment)**
    - Points to the segment containing data.
    - Example:
      ```nasm
      mov ax, ds      ; Move the data segment value into AX
      ```

3. **SS (Stack Segment)**
    - Points to the segment containing the stack.
    - Example:
      ```nasm
      mov ax, ss      ; Move the stack segment value into AX
      ```

4. **ES (Extra Segment)**
    - Used for additional data segment.
    - Example:
      ```nasm
      mov ax, es      ; Move the extra segment value into AX
      ```

5. **FS and GS (Additional Segment Registers)**
    - Used for additional data segments.
    - Example:
      ```nasm
      mov ax, fs      ; Move the FS segment value into AX
      mov ax, gs      ; Move the GS segment value into AX
      ```

## Instruction Pointer

1. **RIP (Instruction Pointer)**
    - Points to the next instruction to be executed.
    - Example:
      ```nasm
      call function   ; Call a function, RIP is updated to the function address
      ```

## Flags Register

1. **RFLAGS (Flags Register)**
    - Contains flags that control the CPU and reflect the outcome of operations.
    - Example:
      ```nasm
      add rax, rbx    ; Add RBX to RAX, update flags
      jz zero_flag    ; Jump if zero flag is set
      ```

These registers are essential for various operations in x64 assembly programming, providing the necessary functionality for arithmetic, data manipulation, control flow, and memory access.