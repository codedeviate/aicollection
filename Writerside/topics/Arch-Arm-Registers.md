# Arm Registers

## General Purpose Registers

1. **R0 - R12 (General Purpose Registers)**
    - Used for various purposes including arithmetic operations, data storage, and function arguments.
    - Example:
      ```nasm
      mov r0, #5      ; Move 5 into R0
      add r1, r0, #3  ; Add 3 to R0 and store the result in R1
      ```

2. **R13 (Stack Pointer, SP)**
    - Points to the top of the stack.
    - Example:
      ```nasm
      push {r0}       ; Push R0 onto the stack
      pop {r1}        ; Pop the top of the stack into R1
      ```

3. **R14 (Link Register, LR)**
    - Stores the return address for function calls.
    - Example:
      ```nasm
      bl function     ; Branch with link to function, LR is set to return address
      bx lr           ; Return from function, jump to address in LR
      ```

4. **R15 (Program Counter, PC)**
    - Points to the next instruction to be executed.
    - Example:
      ```nasm
      b label         ; Branch to label, PC is updated to the address of label
      ```

## Special Purpose Registers

1. **CPSR (Current Program Status Register)**
    - Holds the condition flags (Negative, Zero, Carry, Overflow) and control bits.
    - Example:
      ```nasm
      adds r0, r1, r2 ; Add R1 and R2, update condition flags
      bne not_equal   ; Branch if not equal (Zero flag is not set)
      ```

2. **SPSR (Saved Program Status Register)**
    - Holds the saved state of CPSR when an exception occurs.
    - Example:
      ```nasm
      mrs r0, spsr    ; Move the value of SPSR into R0
      ```

## Floating-Point and SIMD Registers

1. **S0 - S31 (Single-Precision Floating-Point Registers)**
    - Used for single-precision floating-point operations.
    - Example:
      ```nasm
      vadd.f32 s0, s1, s2 ; Add two single-precision floating-point values
      ```

2. **D0 - D31 (Double-Precision Floating-Point Registers)**
    - Used for double-precision floating-point operations.
    - Example:
      ```nasm
      vadd.f64 d0, d1, d2 ; Add two double-precision floating-point values
      ```

3. **Q0 - Q15 (Quadword Registers)**
    - Used for SIMD (Single Instruction, Multiple Data) operations.
    - Example:
      ```nasm
      vadd.i32 q0, q1, q2 ; Add two quadword vectors of 32-bit integers
      ```

These registers are essential for various operations in ARM assembly programming, providing the necessary functionality for arithmetic, data manipulation, control flow, and memory access.