# 6800 Registers

## General Purpose Registers

1. **A (Accumulator)**
    - Used for arithmetic and logic operations.
    - Example:
      ```nasm
      LDA #$10       ; Load immediate value 16 into A
      ADD #$05       ; Add 5 to A, result in A
      ```

2. **B (Accumulator)**
    - Used for arithmetic and logic operations.
    - Example:
      ```nasm
      LDB #$20       ; Load immediate value 32 into B
      SUB #$05       ; Subtract 5 from B, result in B
      ```

## Index Register

1. **X (Index Register)**
    - Used for indexing memory locations.
    - Example:
      ```nasm
      LDX #$1000     ; Load immediate value 4096 into X
      LDA $2000,X    ; Load value from address $2000 + X into A
      ```

## Stack Pointer

1. **SP (Stack Pointer)**
    - Points to the top of the stack.
    - Example:
      ```nasm
      TSX            ; Transfer SP to X
      ```

## Program Counter

1. **PC (Program Counter)**
    - Points to the next instruction to be executed.
    - Example:
      ```nasm
      JMP $3000      ; Jump to address $3000, PC is updated to $3000
      ```

## Condition Code Register

1. **CCR (Condition Code Register)**
    - Contains flags that reflect the outcome of operations and control the CPU.
    - Example:
      ```nasm
      CLC            ; Clear carry flag
      SEC            ; Set carry flag
      ```

These registers are essential for various operations in 6800 assembly programming, providing the necessary functionality for arithmetic, data manipulation, control flow, and memory access.