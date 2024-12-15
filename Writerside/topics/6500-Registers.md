# 6500 Registers

## General Purpose Registers

1. **A (Accumulator)**
    - Used for arithmetic and logic operations.
    - Example:
      ```nasm
      LDA #$10       ; Load immediate value 16 into A
      ADC #$05       ; Add 5 to A, result in A
      ```

2. **X (Index Register X)**
    - Used for indexing memory locations.
    - Example:
      ```nasm
      LDX #$03       ; Load immediate value 3 into X
      LDA $2000,X    ; Load value from address $2000 + X into A
      ```

3. **Y (Index Register Y)**
    - Used for indexing memory locations.
    - Example:
      ```nasm
      LDY #$04       ; Load immediate value 4 into Y
      LDA $2000,Y    ; Load value from address $2000 + Y into A
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

## Status Register

1. **P (Processor Status)**
    - Contains flags that reflect the outcome of operations and control the CPU.
    - Example:
      ```nasm
      CLC            ; Clear carry flag
      SEC            ; Set carry flag
      ```

These registers are essential for various operations in 6500 assembly programming, providing the necessary functionality for arithmetic, data manipulation, control flow, and memory access.