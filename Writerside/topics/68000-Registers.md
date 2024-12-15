# 68000 Registers

## General Purpose Registers

1. **D0 - D7 (Data Registers)**
    - Used for arithmetic, logic operations, and data storage.
    - Example:
      ```nasm
      MOVE.L #10, D0   ; Move immediate value 10 into D0
      ADD.L #5, D0     ; Add 5 to D0, result in D0
      ```

2. **A0 - A7 (Address Registers)**
    - Used for addressing memory locations.
    - Example:
      ```nasm
      LEA $1000, A0    ; Load effective address $1000 into A0
      MOVE.L (A0), D1  ; Move the value at address in A0 into D1
      ```

## Stack Pointer

1. **A7 (User Stack Pointer, USP)**
    - Points to the top of the user stack.
    - Example:
      ```nasm
      MOVE.L A7, USP   ; Move the value of A7 to USP
      ```

2. **SSP (Supervisor Stack Pointer)**
    - Points to the top of the supervisor stack.
    - Example:
      ```nasm
      MOVE.L A7, SSP   ; Move the value of A7 to SSP
      ```

## Program Counter

1. **PC (Program Counter)**
    - Points to the next instruction to be executed.
    - Example:
      ```nasm
      JMP $3000        ; Jump to address $3000, PC is updated to $3000
      ```

## Status Register

1. **SR (Status Register)**
    - Contains condition codes and control bits.
    - Example:
      ```nasm
      ANDI #$F8FF, SR  ; Clear interrupt priority bits in SR
      ```

## Condition Code Register

1. **CCR (Condition Code Register)**
    - Contains condition flags (Negative, Zero, Carry, Overflow, Extend).
    - Example:
      ```nasm
      ADDI.B #1, D0    ; Add 1 to D0, update condition flags in CCR
      ```

These registers are essential for various operations in 68000 assembly programming, providing the necessary functionality for arithmetic, data manipulation, control flow, and memory access.