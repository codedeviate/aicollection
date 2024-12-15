# PowerPC Registers

## General Purpose Registers

1. **R0 - R31 (General Purpose Registers)**
    - Used for various purposes including arithmetic operations, data storage, and function arguments.
    - Example:
      ```nasm
      li r0, 5        ; Load immediate value 5 into R0
      addi r1, r0, 3  ; Add 3 to R0 and store the result in R1
      ```

## Special Purpose Registers

1. **LR (Link Register)**
    - Stores the return address for function calls.
    - Example:
      ```nasm
      bl function     ; Branch with link to function, LR is set to return address
      bclr 20, 0      ; Branch to address in LR
      ```

2. **CTR (Count Register)**
    - Used for loop control and branching.
    - Example:
      ```nasm
      mtctr r3        ; Move the value in R3 to CTR
      bdnz loop       ; Branch to loop if CTR is not zero and decrement CTR
      ```

3. **XER (Fixed-Point Exception Register)**
    - Contains flags for fixed-point arithmetic exceptions.
    - Example:
      ```nasm
      addo r0, r1, r2 ; Add R1 and R2 with overflow detection, update XER
      ```

## Floating-Point Registers

1. **F0 - F31 (Floating-Point Registers)**
    - Used for floating-point operations.
    - Example:
      ```nasm
      lfs f0, 0(r3)   ; Load single-precision floating-point value from memory into F0
      fadds f1, f0, f2 ; Add F0 and F2, store the result in F1
      ```

## Condition Register

1. **CR (Condition Register)**
    - Contains condition flags for branching and comparisons.
    - Example:
      ```nasm
      cmpw r0, r1     ; Compare R0 and R1, update CR
      beq equal       ; Branch to equal if CR indicates equality
      ```

## Program Counter

1. **PC (Program Counter)**
    - Points to the next instruction to be executed.
    - Example:
      ```nasm
      b label         ; Branch to label, PC is updated to the address of label
      ```

These registers are essential for various operations in PowerPC assembly programming, providing the necessary functionality for arithmetic, data manipulation, control flow, and memory access.