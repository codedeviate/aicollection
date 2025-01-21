# Arm Mnemonics

Below is a detailed list of the ARM 32-bit architecture (also known as ARMv7) instructions, with explanations, examples, and usage for each instruction type.

## Data Processing Instructions:
1. **ADD** (Addition)
    - **Description**: Adds two operands and stores the result in the destination register.
    - **Example**: `ADD R0, R1, R2`  
      Adds the values in registers `R1` and `R2`, and stores the result in `R0`.

2. **SUB** (Subtraction)
    - **Description**: Subtracts the second operand from the first operand and stores the result in the destination register.
    - **Example**: `SUB R0, R1, R2`  
      Subtracts the value in `R2` from `R1` and stores the result in `R0`.

3. **RSB** (Reverse Subtraction)
    - **Description**: Performs subtraction in reverse order.
    - **Example**: `RSB R0, R1, R2`  
      Subtracts the value in `R1` from `R2` and stores the result in `R0`.

4. **MUL** (Multiply)
    - **Description**: Multiplies two operands and stores the result in the destination register.
    - **Example**: `MUL R0, R1, R2`  
      Multiplies the values in `R1` and `R2`, and stores the result in `R0`.

5. **SDIV** (Signed Division)
    - **Description**: Divides the first operand by the second operand (signed) and stores the result in the destination register.
    - **Example**: `SDIV R0, R1, R2`  
      Divides the value in `R1` by the value in `R2` (signed division) and stores the result in `R0`.

6. **UDIV** (Unsigned Division)
    - **Description**: Divides the first operand by the second operand (unsigned) and stores the result in the destination register.
    - **Example**: `UDIV R0, R1, R2`  
      Divides the value in `R1` by the value in `R2` (unsigned division) and stores the result in `R0`.

7. **AND** (Bitwise AND)
    - **Description**: Performs a bitwise AND operation between two operands and stores the result in the destination register.
    - **Example**: `AND R0, R1, R2`  
      Performs a bitwise AND between the values in `R1` and `R2`, and stores the result in `R0`.

8. **ORR** (Bitwise OR)
    - **Description**: Performs a bitwise OR operation between two operands and stores the result in the destination register.
    - **Example**: `ORR R0, R1, R2`  
      Performs a bitwise OR between the values in `R1` and `R2`, and stores the result in `R0`.

9. **EOR** (Bitwise XOR)
    - **Description**: Performs a bitwise XOR operation between two operands and stores the result in the destination register.
    - **Example**: `EOR R0, R1, R2`  
      Performs a bitwise XOR between the values in `R1` and `R2`, and stores the result in `R0`.

10. **BIC** (Bitwise Clear)
    - **Description**: Performs a bitwise AND between the first operand and the negation of the second operand and stores the result in the destination register.
    - **Example**: `BIC R0, R1, R2`  
      Performs a bitwise AND between `R1` and the negation of `R2`, and stores the result in `R0`.

11. **TST** (Test)
    - **Description**: Performs a bitwise AND between two operands, but does not store the result; only updates the condition flags.
    - **Example**: `TST R1, R2`  
      Performs a bitwise AND between `R1` and `R2`, updating the flags based on the result.

12. **CMP** (Compare)
    - **Description**: Subtracts the second operand from the first operand, but does not store the result; only updates the condition flags.
    - **Example**: `CMP R1, R2`  
      Subtracts `R2` from `R1` and updates the flags based on the result.

---

## Load and Store Instructions:
1. **LDR** (Load Register)
    - **Description**: Loads data from memory into a register.
    - **Example**: `LDR R0, [R1, #4]`  
      Loads the value from memory at address `R1 + 4` into register `R0`.

2. **STR** (Store Register)
    - **Description**: Stores data from a register into memory.
    - **Example**: `STR R0, [R1, #4]`  
      Stores the value in `R0` into memory at address `R1 + 4`.

3. **LDM** (Load Multiple)
    - **Description**: Loads multiple registers from memory.
    - **Example**: `LDM R0, {R1, R2, R3}`  
      Loads the values from memory into registers `R1`, `R2`, and `R3` starting at address `R0`.

4. **STM** (Store Multiple)
    - **Description**: Stores multiple registers to memory.
    - **Example**: `STM R0, {R1, R2, R3}`  
      Stores the values from registers `R1`, `R2`, and `R3` into memory starting at address `R0`.

5. **LDRB** (Load Byte)
    - **Description**: Loads a byte from memory into a register.
    - **Example**: `LDRB R0, [R1]`  
      Loads a byte from memory at address `R1` into register `R0`.

6. **STRB** (Store Byte)
    - **Description**: Stores a byte from a register into memory.
    - **Example**: `STRB R0, [R1]`  
      Stores a byte from register `R0` into memory at address `R1`.

---

## Branch Instructions:
1. **B** (Branch)
    - **Description**: Performs an unconditional jump to a specified label.
    - **Example**: `B label`  
      Jumps to the instruction at the specified label.

2. **BL** (Branch with Link)
    - **Description**: Performs a branch and stores the return address in the link register (`LR`).
    - **Example**: `BL function`  
      Branches to `function` and saves the return address in `LR`.

3. **BX** (Branch and Exchange)
    - **Description**: Branches to an address stored in a register and optionally switches the processor mode (ARM/Thumb).
    - **Example**: `BX R0`  
      Branches to the address stored in `R0` and switches to the appropriate execution state (ARM or Thumb).

4. **BLX** (Branch with Link and Exchange)
    - **Description**: Performs a branch with link and switches between ARM/Thumb states.
    - **Example**: `BLX R0`  
      Branches to the address in `R0`, saves the return address in `LR`, and switches to the appropriate execution state.

---

## Shift and Rotate Instructions:
1. **LSL** (Logical Shift Left)
    - **Description**: Shifts the bits of a register to the left by a specified number of positions, filling with zeros.
    - **Example**: `LSL R0, R1, #2`  
      Shifts the bits of `R1` left by 2 positions, stores the result in `R0`.

2. **LSR** (Logical Shift Right)
    - **Description**: Shifts the bits of a register to the right by a specified number of positions, filling with zeros.
    - **Example**: `LSR R0, R1, #2`  
      Shifts the bits of `R1` right by 2 positions, stores the result in `R0`.

3. **ASR** (Arithmetic Shift Right)
    - **Description**: Shifts the bits of a register to the right by a specified number of positions, preserving the sign bit (used for signed numbers).
    - **Example**: `ASR R0, R1, #2`  
      Shifts the bits of `R1` right by 2 positions, preserving the sign bit, and stores the result in `R0`.

4. **ROR** (Rotate Right)
    - **Description**: Rotates the bits of a register to the right by a specified number of positions.
    - **Example**: `ROR R0, R1, #2`  
      Rotates the bits of `R1` right by 2 positions, storing the result in `R0`.

---

## Miscellaneous Instructions:
1. **NOP** (No Operation)
    - **Description**: Does nothing and is typically used for timing or padding purposes.
    - **Example**: `NOP`  
      Does nothing.

2. **SWI** (Software Interrupt)
    - **Description**: Triggers a software interrupt, typically used for making system calls.
    - **Example**: `SWI 0`  
      Issues a software interrupt with code 0.

3. **CMP** (Compare)
    - **Description**: Subtracts two operands and updates the condition flags without storing the result.
    - **Example**: `CMP R0, R1`  
      Subtracts `R1` from `R0` and updates the flags based on the result.

4. **TST** (Test)
    - **Description**: Performs a bitwise AND between two operands and updates the condition flags.
    - **Example**: `TST R0, R1`  
      Performs a bitwise AND between `R0` and `R1` and updates the flags.

---

## System Instructions:
1. **MRS** (Move from System Register)
    - **Description**: Moves the value from a system register into a general-purpose register.
    - **Example**: `MRS R0, CPSR`  
      Moves the value of the `CPSR` (Current Program Status Register) into `R0`.

2. **MSR** (Move to System Register)
    - **Description**: Moves a value from a general-purpose register into a system register.
    - **Example**: `MSR CPSR, R0`  
      Moves the value in `R0` into the `CPSR`.

---

This list outlines the key instructions for ARM 32-bit (ARMv7) assembly language, including arithmetic, logic, memory operations, control flow, and system-level instructions. These are fundamental for developing software on ARM-based systems such as mobile devices, embedded systems, and older ARM architectures.