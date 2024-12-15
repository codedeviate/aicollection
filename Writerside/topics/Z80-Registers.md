# Z80 Registers

## General Purpose Registers

1. **A (Accumulator)**
    - Used for arithmetic and logic operations.
    - Example:
      ```nasm
      LD A, 0x10     ; Load immediate value 16 into A
      ADD A, 0x05    ; Add 5 to A, result in A
      ```

2. **B, C, D, E, H, L (8-bit Registers)**
    - Used for general-purpose data storage and manipulation.
    - Example:
      ```nasm
      LD B, 0x03     ; Load immediate value 3 into B
      LD C, 0x04     ; Load immediate value 4 into C
      ```

3. **BC, DE, HL (16-bit Register Pairs)**
    - Used for 16-bit operations and addressing.
    - Example:
      ```nasm
      LD BC, 0x1234  ; Load immediate value 0x1234 into BC
      LD DE, 0x5678  ; Load immediate value 0x5678 into DE
      LD HL, 0x9ABC  ; Load immediate value 0x9ABC into HL
      ```

## Special Purpose Registers

1. **IX, IY (Index Registers)**
    - Used for indexed addressing modes.
    - Example:
      ```nasm
      LD IX, 0x2000  ; Load immediate value 0x2000 into IX
      LD IY, 0x3000  ; Load immediate value 0x3000 into IY
      ```

2. **SP (Stack Pointer)**
    - Points to the top of the stack.
    - Example:
      ```nasm
      LD SP, 0xFFFE  ; Load immediate value 0xFFFE into SP
      ```

3. **PC (Program Counter)**
    - Points to the next instruction to be executed.
    - Example:
      ```nasm
      JP 0x4000      ; Jump to address 0x4000, PC is updated to 0x4000
      ```

4. **F (Flags Register)**
    - Contains flags that reflect the outcome of operations and control the CPU.
    - Example:
      ```nasm
      OR A           ; Logical OR A with itself, sets Zero flag if A is 0
      ```

5. **I (Interrupt Vector Register)**
    - Used for interrupt handling.
    - Example:
      ```nasm
      LD I, 0x38     ; Load immediate value 0x38 into I
      ```

6. **R (Memory Refresh Register)**
    - Used for dynamic RAM refresh.
    - Example:
      ```nasm
      LD R, 0x00     ; Load immediate value 0 into R
      ```

## Alternate Register Set

1. **A', B', C', D', E', H', L', F' (Shadow Registers)**
    - Used for fast context switching.
    - Example:
      ```nasm
      EXX            ; Exchange BC, DE, HL with their shadow registers
      EX AF, AF'     ; Exchange AF with its shadow register
      ```

These registers provide the necessary functionality for arithmetic, data manipulation, control flow, memory access, and interrupt handling in Z80 assembly programming.