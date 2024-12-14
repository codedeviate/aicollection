# 6500

## Overview

The 6500 architecture, also known as the MOS Technology 6502, is an 8-bit microprocessor architecture developed by MOS Technology in 1975. It was widely used in early home computers, video game consoles, and embedded systems due to its low cost and simplicity.

## History of 6500 Architecture

1. **MOS Technology 6502 (1975)**: The original 8-bit processor that started the 6500 architecture.
2. **WDC 65C02 (1982)**: An enhanced version of the 6502 with additional instructions and lower power consumption.
3. **WDC 65816 (1984)**: A 16-bit extension of the 6502, used in systems like the Apple IIGS and the Super Nintendo Entertainment System (SNES).

## Key Concepts

- **8-bit Architecture**: The 6500 architecture is based on an 8-bit data bus, meaning it can process 8 bits of data at a time.
- **Registers**: The 6500 has a small set of registers for operations.
- **Addressing Modes**: The 6500 supports various addressing modes for accessing memory.
- **Simple Instruction Set**: The 6500 has a relatively simple and small instruction set, making it easy to learn and use.

## 6500 Architecture

### Registers

- **Accumulator (A)**: Used for arithmetic and logic operations.
- **Index Registers (X, Y)**: Used for indexing and loop control.
- **Stack Pointer (SP)**: Points to the current position in the stack.
- **Program Counter (PC)**: Points to the next instruction to be executed.
- **Status Register (P)**: Holds the processor status flags.

### Example: Simple Assembly Program

```nasm
    .org $8000
    .db $00, $10, $20, $30, $40, $50, $60, $70, $80, $90, $A0, $B0, $C0, $D0, $E0, $F0

    .org $FFFC
    .dw $8000

    .org $8000
start:
    LDX #$00        ; Load X with 0
loop:
    LDA data, X     ; Load A with data at address (data + X)
    STA $0200, X    ; Store A at address ($0200 + X)
    INX             ; Increment X
    CPX #$10        ; Compare X with 16
    BNE loop        ; Branch to loop if X is not equal to 16
    BRK             ; Break (end of program)

data:
    .db $00, $10, $20, $30, $40, $50, $60, $70, $80, $90, $A0, $B0, $C0, $D0, $E0, $F0
```

## Differences Between 6500 and Other Architectures

- **8-bit vs. 16/32/64-bit**: The 6500 is an 8-bit architecture, while modern architectures like x86 and ARM are 16, 32, or 64-bit.
- **Simple Instruction Set**: The 6500 has a simpler and smaller instruction set compared to more complex architectures like x86.
- **Limited Registers**: The 6500 has fewer registers compared to modern architectures, which have more general-purpose and special-purpose registers.

Understanding the 6500 architecture is crucial for low-level programming, performance optimization, and system development in environments where 6500 processors are used.