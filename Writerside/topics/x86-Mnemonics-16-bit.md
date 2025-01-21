# x86 Mnemonics 16-bit

The Intel 80286 is a 16-bit microprocessor that introduced several instructions and features which were crucial for the development of modern x86 processors. Below is a detailed list of the key instructions and their descriptions, examples, and usage for the 80286 architecture.

## Data Processing Instructions:
1. **ADD** (Addition)
    - **Description**: Adds two operands and stores the result in the destination operand.
    - **Example**: `ADD AX, BX`  
      Adds the value in `BX` to `AX`, storing the result in `AX`.

2. **SUB** (Subtraction)
    - **Description**: Subtracts the second operand from the first operand and stores the result in the destination operand.
    - **Example**: `SUB AX, BX`  
      Subtracts the value in `BX` from `AX` and stores the result in `AX`.

3. **MUL** (Unsigned Multiplication)
    - **Description**: Multiplies the accumulator register (`AX`) by the operand, storing the result in `DX:AX`.
    - **Example**: `MUL BX`  
      Multiplies the value in `AX` by `BX`, storing the result in `DX:AX`.

4. **IMUL** (Signed Multiplication)
    - **Description**: Multiplies the accumulator register (`AX`) by the operand, storing the result in `DX:AX` (signed).
    - **Example**: `IMUL AX, BX`  
      Multiplies the value in `AX` by `BX`, storing the result in `DX:AX`.

5. **DIV** (Unsigned Division)
    - **Description**: Divides the value in `DX:AX` by the operand, storing the quotient in `AX` and the remainder in `DX`.
    - **Example**: `DIV BX`  
      Divides the value in `DX:AX` by `BX`, storing the quotient in `AX` and the remainder in `DX`.

6. **IDIV** (Signed Division)
    - **Description**: Divides the value in `DX:AX` by the operand (signed division), storing the quotient in `AX` and the remainder in `DX`.
    - **Example**: `IDIV BX`  
      Divides the value in `DX:AX` by `BX`, storing the quotient in `AX` and the remainder in `DX`.

7. **INC** (Increment)
    - **Description**: Increments the operand by 1.
    - **Example**: `INC AX`  
      Increments the value in `AX` by 1.

8. **DEC** (Decrement)
    - **Description**: Decrements the operand by 1.
    - **Example**: `DEC AX`  
      Decrements the value in `AX` by 1.

9. **AND** (Bitwise AND)
    - **Description**: Performs a bitwise AND between two operands and stores the result in the destination operand.
    - **Example**: `AND AX, BX`  
      Performs a bitwise AND between `AX` and `BX`, storing the result in `AX`.

10. **OR** (Bitwise OR)
    - **Description**: Performs a bitwise OR between two operands and stores the result in the destination operand.
    - **Example**: `OR AX, BX`  
      Performs a bitwise OR between `AX` and `BX`, storing the result in `AX`.

11. **XOR** (Bitwise XOR)
    - **Description**: Performs a bitwise XOR between two operands and stores the result in the destination operand.
    - **Example**: `XOR AX, BX`  
      Performs a bitwise XOR between `AX` and `BX`, storing the result in `AX`.

12. **NOT** (Bitwise NOT)
    - **Description**: Performs a bitwise NOT (inversion) of the operand.
    - **Example**: `NOT AX`  
      Performs a bitwise NOT on `AX`, inverting all bits.

13. **NEG** (Negate)
    - **Description**: Negates the operand (computes the two's complement).
    - **Example**: `NEG AX`  
      Negates the value in `AX`.

---

## Shift and Rotate Instructions:
1. **SHL** (Shift Left)
    - **Description**: Shifts the bits of the operand to the left, inserting zeros into the least significant bits.
    - **Example**: `SHL AX, 1`  
      Shifts the bits of `AX` to the left by 1, filling with zeros.

2. **SHR** (Shift Right)
    - **Description**: Shifts the bits of the operand to the right, inserting zeros into the most significant bits.
    - **Example**: `SHR AX, 1`  
      Shifts the bits of `AX` to the right by 1, filling with zeros.

3. **ROL** (Rotate Left)
    - **Description**: Rotates the bits of the operand to the left.
    - **Example**: `ROL AX, 1`  
      Rotates the bits of `AX` to the left by 1.

4. **ROR** (Rotate Right)
    - **Description**: Rotates the bits of the operand to the right.
    - **Example**: `ROR AX, 1`  
      Rotates the bits of `AX` to the right by 1.

---

## Load and Store Instructions:
1. **MOV** (Move)
    - **Description**: Copies data from one operand to another.
    - **Example**: `MOV AX, BX`  
      Copies the value in `BX` to `AX`.

2. **PUSH** (Push onto stack)
    - **Description**: Pushes a value onto the stack.
    - **Example**: `PUSH AX`  
      Pushes the value in `AX` onto the stack.

3. **POP** (Pop from stack)
    - **Description**: Pops a value from the stack into a register.
    - **Example**: `POP AX`  
      Pops the top value from the stack into `AX`.

4. **LEA** (Load Effective Address)
    - **Description**: Loads the effective address of a memory operand into a register.
    - **Example**: `LEA AX, [BX + 4]`  
      Loads the address calculated from `BX + 4` into `AX`.

5. **MOVZX** (Move with Zero Extension)
    - **Description**: Moves a value and zero-extends it to a larger size.
    - **Example**: `MOVZX AX, BYTE [BX]`  
      Moves the byte at the memory address in `BX` into `AX`, zero-extending it.

6. **MOVSX** (Move with Sign Extension)
    - **Description**: Moves a value and sign-extends it to a larger size.
    - **Example**: `MOVSX AX, BYTE [BX]`  
      Moves the byte at the memory address in `BX` into `AX`, sign-extending it.

---

## Branch Instructions:
1. **JMP** (Jump)
    - **Description**: Unconditionally jumps to a target address.
    - **Example**: `JMP label`  
      Jumps to the instruction at the label.

2. **JE** (Jump if Equal)
    - **Description**: Jumps to a target address if the zero flag is set (i.e., if the two operands were equal).
    - **Example**: `JE label`  
      Jumps to the label if the zero flag is set.

3. **JNE** (Jump if Not Equal)
    - **Description**: Jumps to a target address if the zero flag is cleared (i.e., if the operands were not equal).
    - **Example**: `JNE label`  
      Jumps to the label if the zero flag is cleared.

4. **JL** (Jump if Less)
    - **Description**: Jumps to a target address if the signed comparison is less.
    - **Example**: `JL label`  
      Jumps to the label if the signed comparison is less.

5. **JLE** (Jump if Less or Equal)
    - **Description**: Jumps to a target address if the signed comparison is less or equal.
    - **Example**: `JLE label`  
      Jumps to the label if the signed comparison is less or equal.

6. **JGE** (Jump if Greater or Equal)
    - **Description**: Jumps to a target address if the signed comparison is greater or equal.
    - **Example**: `JGE label`  
      Jumps to the label if the signed comparison is greater or equal.

7. **JMP** (Jump)
    - **Description**: An unconditional jump to a specified address.
    - **Example**: `JMP label`  
      Jumps to `label` unconditionally.

---

## Comparison Instructions:
1. **CMP** (Compare)
    - **Description**: Compares two operands by subtracting them and updating the flags.
    - **Example**: `CMP AX, BX`  
      Compares the values in `AX` and `BX`.

2. **TEST** (Test)
    - **Description**: Performs a bitwise AND between two operands and updates the flags.
    - **Example**: `TEST AX, BX`  
      Performs a bitwise AND between `AX` and `BX` and updates the flags.

---

## Stack Management Instructions:
1. **CALL** (Call Function)
    - **Description**: Calls a function, pushing the return address onto the stack.
    - **Example**: `CALL func`  
      Calls the function `func`.

2. **RET** (Return from Function)
    - **Description**: Pops the return address from the stack and returns to that address.
    - **Example**: `RET`  
      Pops the return address and returns to it.

---

## Miscellaneous Instructions:
1. **NOP** (No Operation)
    - **Description**: Does nothing; typically used for padding or alignment.
    - **Example**: `NOP`  
      No operation.

2. **HLT** (Halt)
    - **Description**: Stops the processor.
    - **Example**: `HLT`  
      Halts execution.

3. **CLD** (Clear Direction Flag)
    - **Description**: Clears the direction flag, ensuring string operations auto-increment addresses.
    - **Example**: `CLD`  
      Clears the direction flag.

4. **STD** (Set Direction Flag)
    - **Description**: Sets the direction flag, ensuring string operations auto-decrement addresses.
    - **Example**: `STD`  
      Sets the direction flag.

---

## System Instructions:
1. **SYSENTER** (System Enter)
    - **Description**: Used for fast system calls.
    - **Example**: `SYSENTER`

2. **SYSCALL** (System Call)
    - **Description**: Triggers a system call.
    - **Example**: `SYSCALL`  
      Issues a system call to the operating system.

---

This list provides an overview of the key 80286 instructions, including arithmetic, logic, shifts, branching, stack management, and system calls. The 80286 is more limited compared to modern x86 processors, but it introduced essential features such as protected mode, which paved the way for more advanced processor architectures.