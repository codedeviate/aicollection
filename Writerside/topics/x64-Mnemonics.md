# x64 Mnemonics

Here is a detailed list of x86_64 mnemonics along with their descriptions, examples, and usage:

## Data Processing Instructions:
1. **ADD** (Addition)
    - **Description**: Adds two operands and stores the result in the destination operand.
    - **Example**: `ADD RAX, RBX`  
      Adds the value in `RBX` to `RAX`, storing the result in `RAX`.

2. **SUB** (Subtraction)
    - **Description**: Subtracts the second operand from the first operand and stores the result in the destination operand.
    - **Example**: `SUB RAX, RBX`  
      Subtracts the value in `RBX` from `RAX` and stores the result in `RAX`.

3. **MUL** (Unsigned Multiplication)
    - **Description**: Multiplies the accumulator register (`RAX`/`EAX`/`AX`) by the operand, storing the result in `RDX:RAX`.
    - **Example**: `MUL RBX`  
      Multiplies the value in `RAX` by `RBX`, storing the result in `RDX:RAX`.

4. **IMUL** (Signed Multiplication)
    - **Description**: Multiplies the accumulator register (`RAX`/`EAX`/`AX`) by the operand, storing the result in `RDX:RAX` (signed).
    - **Example**: `IMUL RAX, RBX`  
      Multiplies the value in `RAX` by `RBX`, storing the result in `RDX:RAX`.

5. **DIV** (Unsigned Division)
    - **Description**: Divides the value in the accumulator register (`RDX:RAX`) by the operand and stores the result in `RAX` (quotient) and `RDX` (remainder).
    - **Example**: `DIV RBX`  
      Divides the value in `RDX:RAX` by `RBX`, storing the quotient in `RAX` and the remainder in `RDX`.

6. **IDIV** (Signed Division)
    - **Description**: Divides the value in the accumulator register (`RDX:RAX`) by the operand (signed division), storing the quotient in `RAX` and the remainder in `RDX`.
    - **Example**: `IDIV RBX`  
      Divides the value in `RDX:RAX` by `RBX`, storing the quotient in `RAX` and the remainder in `RDX`.

7. **INC** (Increment)
    - **Description**: Increments the operand by 1.
    - **Example**: `INC RAX`  
      Increments the value in `RAX` by 1.

8. **DEC** (Decrement)
    - **Description**: Decrements the operand by 1.
    - **Example**: `DEC RAX`  
      Decrements the value in `RAX` by 1.

9. **AND** (Bitwise AND)
    - **Description**: Performs a bitwise AND between two operands and stores the result in the destination operand.
    - **Example**: `AND RAX, RBX`  
      Performs a bitwise AND between `RAX` and `RBX`, storing the result in `RAX`.

10. **OR** (Bitwise OR)
    - **Description**: Performs a bitwise OR between two operands and stores the result in the destination operand.
    - **Example**: `OR RAX, RBX`  
      Performs a bitwise OR between `RAX` and `RBX`, storing the result in `RAX`.

11. **XOR** (Bitwise XOR)
    - **Description**: Performs a bitwise XOR between two operands and stores the result in the destination operand.
    - **Example**: `XOR RAX, RBX`  
      Performs a bitwise XOR between `RAX` and `RBX`, storing the result in `RAX`.

12. **NOT** (Bitwise NOT)
    - **Description**: Performs a bitwise NOT (inversion) of the operand.
    - **Example**: `NOT RAX`  
      Performs a bitwise NOT on `RAX`, inverting all bits.

13. **NEG** (Negate)
    - **Description**: Negates the operand (computes the two's complement).
    - **Example**: `NEG RAX`  
      Negates the value in `RAX`.

---

## Shift and Rotate Instructions:
1. **SHL** (Shift Left)
    - **Description**: Shifts the bits of the operand to the left, inserting zeros into the least significant bits.
    - **Example**: `SHL RAX, 1`  
      Shifts the bits of `RAX` to the left by 1, filling with zeros.

2. **SHR** (Shift Right)
    - **Description**: Shifts the bits of the operand to the right, inserting zeros into the most significant bits.
    - **Example**: `SHR RAX, 1`  
      Shifts the bits of `RAX` to the right by 1, filling with zeros.

3. **SAR** (Arithmetic Shift Right)
    - **Description**: Shifts the bits of the operand to the right, preserving the sign bit (for signed integers).
    - **Example**: `SAR RAX, 1`  
      Shifts the bits of `RAX` to the right by 1, preserving the sign bit.

4. **ROL** (Rotate Left)
    - **Description**: Rotates the bits of the operand to the left.
    - **Example**: `ROL RAX, 1`  
      Rotates the bits of `RAX` to the left by 1.

5. **ROR** (Rotate Right)
    - **Description**: Rotates the bits of the operand to the right.
    - **Example**: `ROR RAX, 1`  
      Rotates the bits of `RAX` to the right by 1.

---

## Load and Store Instructions:
1. **MOV** (Move)
    - **Description**: Copies data from one operand to another.
    - **Example**: `MOV RAX, RBX`  
      Copies the value in `RBX` to `RAX`.

2. **PUSH** (Push onto stack)
    - **Description**: Pushes a value onto the stack.
    - **Example**: `PUSH RAX`  
      Pushes the value in `RAX` onto the stack.

3. **POP** (Pop from stack)
    - **Description**: Pops a value from the stack into a register.
    - **Example**: `POP RAX`  
      Pops the top value from the stack into `RAX`.

4. **LEA** (Load Effective Address)
    - **Description**: Loads the effective address of a memory operand into a register.
    - **Example**: `LEA RAX, [RBX + RCX*4]`  
      Loads the address calculated from `RBX + RCX*4` into `RAX`.

5. **MOVZX** (Move with Zero Extension)
    - **Description**: Moves a value and zero-extends it to a larger size.
    - **Example**: `MOVZX RAX, BYTE [RBX]`  
      Moves the byte at the memory address in `RBX` into `RAX`, zero-extending it.

6. **MOVSX** (Move with Sign Extension)
    - **Description**: Moves a value and sign-extends it to a larger size.
    - **Example**: `MOVSX RAX, BYTE [RBX]`  
      Moves the byte at the memory address in `RBX` into `RAX`, sign-extending it.

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
    - **Example**: `CMP RAX, RBX`  
      Compares the values in `RAX` and `RBX`.

2. **TEST** (Test)
    - **Description**: Performs a bitwise AND between two operands and updates the flags.
    - **Example**: `TEST RAX, RBX`  
      Performs a bitwise AND between `RAX` and `RBX` and updates the flags.

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

This list covers a wide range of x86_64 mnemonics, including instructions for arithmetic, logic, shifts, branching, stack management, system calls, and more.