# Aarch64 Mnemonics

Here is an expanded documentation of the AArch64 mnemonics, including descriptions and example usage for each type of instruction:

## Data Processing Instructions:
1. **ADD** (Addition)
    - **Description**: Adds the values of two registers or a register and an immediate value, storing the result in a destination register.
    - **Example**: `ADD X0, X1, X2`  
      Adds the values in registers `X1` and `X2`, stores the result in `X0`.

2. **SUB** (Subtraction)
    - **Description**: Subtracts the value of one register from another register or subtracts an immediate from a register, storing the result in the destination register.
    - **Example**: `SUB X0, X1, X2`  
      Subtracts the value in `X2` from `X1` and stores the result in `X0`.

3. **MUL** (Multiplication)
    - **Description**: Multiplies the values in two registers and stores the result in a destination register.
    - **Example**: `MUL X0, X1, X2`  
      Multiplies the values in `X1` and `X2`, stores the result in `X0`.

4. **SDIV** (Signed Division)
    - **Description**: Divides the value in one register by the value in another register, using signed integer division.
    - **Example**: `SDIV X0, X1, X2`  
      Divides the signed value in `X1` by the signed value in `X2` and stores the result in `X0`.

5. **UDIV** (Unsigned Division)
    - **Description**: Divides the value in one register by the value in another register, using unsigned integer division.
    - **Example**: `UDIV X0, X1, X2`  
      Divides the unsigned value in `X1` by the unsigned value in `X2` and stores the result in `X0`.

6. **SMULH** (Signed Multiply High)
    - **Description**: Performs a signed multiplication of two 64-bit values and stores the upper 64 bits of the result.
    - **Example**: `SMULH X0, X1, X2`  
      Multiplies the values in `X1` and `X2` (signed), and stores the high 64 bits of the result in `X0`.

7. **UMULH** (Unsigned Multiply High)
    - **Description**: Performs an unsigned multiplication of two 64-bit values and stores the upper 64 bits of the result.
    - **Example**: `UMULH X0, X1, X2`  
      Multiplies the values in `X1` and `X2` (unsigned), and stores the high 64 bits of the result in `X0`.

8. **MLS** (Multiply-Subtract)
    - **Description**: Multiplies two values and then subtracts the third value from the product.
    - **Example**: `MLS X0, X1, X2, X3`  
      Multiplies `X1` and `X2`, then subtracts `X3` from the result, storing the result in `X0`.

9. **UMUL** (Unsigned Multiply)
    - **Description**: Multiplies two unsigned values and stores the result.
    - **Example**: `UMUL X0, X1, X2`  
      Multiplies the unsigned values in `X1` and `X2`, and stores the result in `X0`.

10. **ADC** (Add with Carry)
    - **Description**: Adds two values and the carry flag, storing the result in the destination register.
    - **Example**: `ADC X0, X1, X2`  
      Adds the values in `X1` and `X2`, along with the carry flag, and stores the result in `X0`.

11. **SBC** (Subtract with Carry)
    - **Description**: Subtracts one value from another and subtracts the borrow flag.
    - **Example**: `SBC X0, X1, X2`  
      Subtracts the value in `X2` from `X1` and subtracts the carry flag, storing the result in `X0`.

---

## Load and Store Instructions:
1. **LDR** (Load Register)
    - **Description**: Loads a value from memory into a register.
    - **Example**: `LDR X0, [X1, #4]`  
      Loads the value from memory at the address in `X1 + 4` into register `X0`.

2. **STR** (Store Register)
    - **Description**: Stores the value from a register into memory.
    - **Example**: `STR X0, [X1, #4]`  
      Stores the value in `X0` into memory at the address `X1 + 4`.

3. **LDP** (Load Pair of Registers)
    - **Description**: Loads two registers from consecutive memory addresses.
    - **Example**: `LDP X0, X1, [X2]`  
      Loads two consecutive values from memory starting at the address in `X2` into registers `X0` and `X1`.

4. **STP** (Store Pair of Registers)
    - **Description**: Stores two registers to consecutive memory addresses.
    - **Example**: `STP X0, X1, [X2]`  
      Stores the values in `X0` and `X1` into memory at the address in `X2`.

5. **LDRB** (Load Byte)
    - **Description**: Loads a byte (8 bits) from memory into a register.
    - **Example**: `LDRB W0, [X1]`  
      Loads a byte from memory at the address in `X1` into register `W0`.

6. **STRB** (Store Byte)
    - **Description**: Stores a byte (8 bits) from a register into memory.
    - **Example**: `STRB W0, [X1]`  
      Stores the byte in `W0` into memory at the address in `X1`.

7. **LDRH** (Load Halfword)
    - **Description**: Loads a halfword (16 bits) from memory into a register.
    - **Example**: `LDRH W0, [X1]`  
      Loads a halfword from memory at the address in `X1` into register `W0`.

8. **STRH** (Store Halfword)
    - **Description**: Stores a halfword (16 bits) from a register into memory.
    - **Example**: `STRH W0, [X1]`  
      Stores the halfword in `W0` into memory at the address in `X1`.

9. **LDUR** (Load Register Unscaled)
    - **Description**: Loads a value from memory into a register using an unscaled offset.
    - **Example**: `LDUR X0, [X1, #4]`  
      Loads the value from memory at address `X1 + 4` into register `X0`.

10. **STUR** (Store Register Unscaled)
    - **Description**: Stores a register value into memory using an unscaled offset.
    - **Example**: `STUR X0, [X1, #4]`  
      Stores the value in `X0` into memory at address `X1 + 4`.

11. **LDRSW** (Load Signed Word)
    - **Description**: Loads a signed word from memory and sign-extends it to 64 bits.
    - **Example**: `LDRSW X0, [X1]`  
      Loads a signed word from memory at the address in `X1` into `X0`.

---

## Branch Instructions:
1. **B** (Branch)
    - **Description**: Unconditionally branches to a specified address or label.
    - **Example**: `B label`  
      Branches to the location specified by the label.

2. **BL** (Branch with Link)
    - **Description**: Branches to a specified address, saving the return address (the address of the next instruction) in the link register (LR).
    - **Example**: `BL func`  
      Branches to the function `func`, storing the return address in the link register.

3. **BR** (Branch Register)
    - **Description**: Branches to the address stored in a register.
    - **Example**: `BR X0`  
      Branches to the address stored in register `X0`.

4. **CBZ** (Compare and Branch on Zero)
    - **Description**: Compares the value in a register to zero and branches if equal.
    - **Example**: `CBZ X0, label`  
      Branches to the label if the value in `X0` is zero.

5. **CBNZ** (Compare and Branch on Non-Zero)
    - **Description**: Compares the value in a register to zero and branches if not equal.
    - **Example**: `CBNZ X0, label`  
      Branches to the label if the value in `X0` is not zero.

6. **TBZ** (Test Bit and Branch on Zero)
    - **Description**: Tests a specific bit in a register and branches if that bit is zero.
    - **Example**: `TBZ X0, #2, label`  
      Branches to the label if bit 2 in `X0` is zero.

7. **TBNZ** (Test Bit and Branch on Non-Zero)
    - **Description**: Tests a specific bit in a register and branches if that bit is non-zero.
    - **Example**: `TBNZ X0, #2, label`  
      Branches to the label if bit 2 in `X0` is non-zero.

---

## Logical and Comparison Instructions:
1. **AND** (Bitwise AND)
    - **Description**: Performs a bitwise AND operation between two registers or between a register and an immediate value.
    - **Example**: `AND X0, X1, X2`  
      Performs a bitwise AND between the values in `X1` and `X2`, and stores the result in `X0`.

2. **ORR** (Bitwise OR)
    - **Description**: Performs a bitwise OR operation between two registers or between a register and an immediate value.
    - **Example**: `ORR X0, X1, X2`  
      Performs a bitwise OR between the values in `X1` and `X2`, and stores the result in `X0`.

3. **EOR** (Bitwise XOR)
    - **Description**: Performs a bitwise XOR operation between two registers or between a register and an immediate value.
    - **Example**: `EOR X0, X1, X2`  
      Performs a bitwise XOR between the values in `X1` and `X2`, and stores the result in `X0`.

4. **BIC** (Bitwise Clear)
    - **Description**: Performs a bitwise AND between the first operand and the negation of the second operand.
    - **Example**: `BIC X0, X1, X2`  
      Performs a bitwise AND between the value in `X1` and the negation of `X2`, and stores the result in `X0`.

5. **ANDS** (Bitwise AND with Condition Flags)
    - **Description**: Performs a bitwise AND and updates the condition flags based on the result.
    - **Example**: `ANDS X0, X1, X2`  
      Performs a bitwise AND between `X1` and `X2` and updates the flags.

6. **ORN** (Bitwise OR NOT)
    - **Description**: Performs a bitwise OR between the first operand and the negation of the second operand.
    - **Example**: `ORN X0, X1, X2`  
      Performs a bitwise OR between `X1` and the negation of `X2`, and stores the result in `X0`.

7. **CMP** (Compare)
    - **Description**: Compares two values by subtracting them and updating the flags accordingly.
    - **Example**: `CMP X1, X2`  
      Compares the values in `X1` and `X2` and updates the flags.

8. **TST** (Test Bits)
    - **Description**: Tests specific bits in a register by performing a bitwise AND and updating the flags.
    - **Example**: `TST X1, #1`  
      Tests if the least significant bit of `X1` is set.

---

## Shift and Rotate Instructions:
1. **LSL** (Logical Shift Left)
    - **Description**: Shifts the bits in a register to the left, inserting zeros in the least significant bits.
    - **Example**: `LSL X0, X1, #4`  
      Shifts the bits in `X1` left by 4 positions and stores the result in `X0`.

2. **LSR** (Logical Shift Right)
    - **Description**: Shifts the bits in a register to the right, inserting zeros in the most significant bits.
    - **Example**: `LSR X0, X1, #4`  
      Shifts the bits in `X1` right by 4 positions and stores the result in `X0`.

3. **ASR** (Arithmetic Shift Right)
    - **Description**: Shifts the bits in a register to the right, maintaining the sign bit (for signed integers).
    - **Example**: `ASR X0, X1, #4`  
      Shifts the bits in `X1` right by 4 positions, performing sign extension, and stores the result in `X0`.

4. **ROR** (Rotate Right)
    - **Description**: Rotates the bits in a register to the right, wrapping around the least significant bits.
    - **Example**: `ROR X0, X1, #4`  
      Rotates the bits in `X1` right by 4 positions and stores the result in `X0`.

---

## Floating Point and SIMD Instructions:
1. **FMUL** (Floating-Point Multiply)
    - **Description**: Multiplies two floating-point values and stores the result.
    - **Example**: `FMUL S0, S1, S2`  
      Multiplies the floating-point values in `S1` and `S2`, and stores the result in `S0`.

2. **FADD** (Floating-Point Add)
    - **Description**: Adds two floating-point values and stores the result.
    - **Example**: `FADD S0, S1, S2`  
      Adds the floating-point values in `S1` and `S2`, and stores the result in `S0`.

3. **FDIV** (Floating-Point Divide)
    - **Description**: Divides one floating-point value by another and stores the result.
    - **Example**: `FDIV S0, S1, S2`  
      Divides the floating-point value in `S1` by the floating-point value in `S2`, and stores the result in `S0`.

4. **FSUB** (Floating-Point Subtract)
    - **Description**: Subtracts one floating-point value from another and stores the result.
    - **Example**: `FSUB S0, S1, S2`  
      Subtracts the floating-point value in `S2` from `S1`, and stores the result in `S0`.

5. **FMADD** (Floating-Point Multiply-Add)
    - **Description**: Multiplies two floating-point values and then adds a third value.
    - **Example**: `FMADD S0, S1, S2, S3`  
      Multiplies `S1` and `S2`, and adds `S3` to the result, storing the result in `S0`.

6. **FMSUB** (Floating-Point Multiply-Subtract)
    - **Description**: Multiplies two floating-point values and then subtracts a third value.
    - **Example**: `FMSUB S0, S1, S2, S3`  
      Multiplies `S1` and `S2`, and subtracts `S3` from the result, storing the result in `S0`.

7. **FNMADD** (Floating-Point Negate Multiply-Add)
    - **Description**: Negates the product of two floating-point values and adds a third.
    - **Example**: `FNMADD S0, S1, S2, S3`  
      Negates the product of `S1` and `S2`, and adds `S3` to the result, storing the result in `S0`.

8. **FNMSUB** (Floating-Point Negate Multiply-Subtract)
    - **Description**: Negates the product of two floating-point values and subtracts a third.
    - **Example**: `FNMSUB S0, S1, S2, S3`  
      Negates the product of `S1` and `S2`, and subtracts `S3` from the result, storing the result in `S0`.

---

## Miscellaneous Instructions:
1. **NOP** (No Operation)
    - **Description**: Does nothing. Used for padding or timing purposes.
    - **Example**: `NOP`

2. **HLT** (Halt)
    - **Description**: Halts execution of the program.
    - **Example**: `HLT #0`

3. **MOV** (Move)
    - **Description**: Moves an immediate value or the contents of a register to a destination register.
    - **Example**: `MOV X0, #10`  
      Moves the immediate value `10` into `X0`.

4. **MOVZ** (Move Zero-Extended)
    - **Description**: Moves an immediate value into a register, zero-extending it to the register width.
    - **Example**: `MOVZ X0, #10`  
      Moves the immediate value `10` into `X0` with zero extension.

5. **MOVK** (Move with Constant)
    - **Description**: Moves an immediate value into a register, replacing a specified portion of the register's value.
    - **Example**: `MOVK X0, #10`  
      Moves the immediate value `10` into `X0` with constant replacement.

6. **MOVN** (Move with Negation)
    - **Description**: Moves a negated immediate value into a register.


- **Example**: `MOVN X0, #10`  
  Moves the negated immediate value `-10` into `X0`.

7. **SVC** (Supervisor Call)
    - **Description**: Triggers a system call (often used for exception handling).
    - **Example**: `SVC #0`  
      Issues a supervisor call with the immediate value `0`.

---

## System Instructions:
1. **MRS** (Move from System Register)
    - **Description**: Copies the value from a system register into a general-purpose register.
    - **Example**: `MRS X0, NZCV`  
      Moves the condition flags from the `NZCV` system register into `X0`.

2. **MSR** (Move to System Register)
    - **Description**: Writes the value from a general-purpose register to a system register.
    - **Example**: `MSR NZCV, X0`  
      Moves the value in `X0` into the `NZCV` system register.

3. **ISB** (Instruction Synchronization Barrier)
    - **Description**: Synchronizes the pipeline by ensuring all prior instructions are completed before proceeding.
    - **Example**: `ISB`

---

## Exception Handling Instructions:
1. **BRK** (Break)
    - **Description**: Triggers a breakpoint exception for debugging.
    - **Example**: `BRK #0`

2. **DFG** (Data Fault Generation)
    - **Description**: Generates a data fault exception.
    - **Example**: `DFG`

This detailed documentation covers many of the essential instructions in AArch64.