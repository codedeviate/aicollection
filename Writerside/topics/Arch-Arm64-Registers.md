# Arm64 Registers

## General Purpose Registers

1. **X0 - X30 (General Purpose Registers)**
    - Used for various purposes including function arguments, return values, and general data storage.
    - Example:
      ```nasm
      mov x0, 5      ; Move 5 into X0
      add x1, x0, 3  ; Add 3 to X0 and store the result in X1
      ```

2. **XZR (Zero Register)**
    - Always reads as zero and writes are discarded.
    - Example:
      ```nasm
      mov x0, xzr    ; Move 0 into X0
      ```

3. **SP (Stack Pointer)**
    - Points to the top of the stack.
    - Example:
      ```nasm
      stp x29, x30, [sp, #-16]! ; Push X29 and X30 onto the stack
      ldp x29, x30, [sp], #16   ; Pop X29 and X30 from the stack
      ```

4. **FP (Frame Pointer)**
    - Points to the base of the current stack frame.
    - Example:
      ```nasm
      mov x29, sp    ; Set frame pointer to the current stack pointer
      ```

5. **LR (Link Register)**
    - Stores the return address for function calls.
    - Example:
      ```nasm
      bl function    ; Branch with link to function, LR is set to return address
      ret            ; Return from function, jump to address in LR
      ```

## Special Purpose Registers

1. **PC (Program Counter)**
    - Points to the next instruction to be executed.
    - Example:
      ```nasm
      b label        ; Branch to label, PC is updated to the address of label
      ```

2. **NZCV (Condition Flags)**
    - Holds the condition flags (Negative, Zero, Carry, Overflow).
    - Example:
      ```nasm
      adds x0, x1, x2 ; Add X1 and X2, update condition flags
      b.eq equal      ; Branch to equal if the zero flag is set
      ```

## SIMD and Floating-Point Registers

1. **V0 - V31 (Vector Registers)**
    - Used for SIMD (Single Instruction, Multiple Data) and floating-point operations.
    - Example:
      ```nasm
      fadd v0.2s, v1.2s, v2.2s ; Add two single-precision floating-point vectors
      ```

These registers are essential for various operations in ARM64 assembly programming, providing the necessary functionality for arithmetic, data manipulation, control flow, and memory access.