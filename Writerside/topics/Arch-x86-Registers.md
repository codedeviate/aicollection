# x86 Registers

## General Purpose Registers

1. **EAX (Accumulator Register)**
    - Used for arithmetic operations.
    - Example:
      ```nasm
      mov eax, 5      ; Move 5 into EAX
      add eax, 3      ; Add 3 to EAX, EAX now contains 8
      ```

2. **EBX (Base Register)**
    - Used as a base pointer for memory access.
    - Example:
      ```nasm
      mov ebx, 0x1000 ; Move address 0x1000 into EBX
      mov eax, [ebx]  ; Move the value at address 0x1000 into EAX
      ```

3. **ECX (Counter Register)**
    - Used for loop operations and string operations.
    - Example:
      ```nasm
      mov ecx, 10     ; Set loop counter to 10
      loop_start:
      ; Loop body
      loop loop_start ; Decrement ECX and jump to loop_start if ECX is not zero
      ```

4. **EDX (Data Register)**
    - Used for I/O operations and arithmetic operations.
    - Example:
      ```nasm
      mov eax, 10
      mov edx, 2
      mul edx         ; Multiply EAX by EDX, result in EAX, high-order bits in EDX
      ```

5. **ESI (Source Index)**
    - Used for string and array operations.
    - Example:
      ```nasm
      mov esi, source ; Point ESI to the source array
      mov edi, dest   ; Point EDI to the destination array
      mov ecx, length ; Set the length of the array
      rep movsb       ; Copy bytes from [ESI] to [EDI], ECX times
      ```

6. **EDI (Destination Index)**
    - Used for string and array operations.
    - Example:
      ```nasm
      mov esi, source ; Point ESI to the source array
      mov edi, dest   ; Point EDI to the destination array
      mov ecx, length ; Set the length of the array
      rep movsb       ; Copy bytes from [ESI] to [EDI], ECX times
      ```

7. **EBP (Base Pointer)**
    - Used to point to the base of the stack frame.
    - Example:
      ```nasm
      push ebp        ; Save old base pointer
      mov ebp, esp    ; Set new base pointer
      sub esp, 16     ; Allocate 16 bytes on the stack
      ```

8. **ESP (Stack Pointer)**
    - Points to the top of the stack.
    - Example:
      ```nasm
      push eax        ; Push EAX onto the stack
      pop ebx         ; Pop the top of the stack into EBX
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

1. **EIP (Instruction Pointer)**
    - Points to the next instruction to be executed.
    - Example:
      ```nasm
      call function   ; Call a function, EIP is updated to the function address
      ```

## Flags Register

1. **EFLAGS (Flags Register)**
    - Contains flags that control the CPU and reflect the outcome of operations.
    - Example:
      ```nasm
      add eax, ebx    ; Add EBX to EAX, update flags
      jz zero_flag    ; Jump if zero flag is set
      ```

These registers are essential for various operations in x86 assembly programming, providing the necessary functionality for arithmetic, data manipulation, control flow, and memory access.