# x86 Mnemonics 32-bit

Here is a detailed list of x86 instructions (32-bit architecture), with explanations, examples, and usage.

## Data Processing Instructions:
1. **ADD** (Addition)
    - **Description**: Adds two operands and stores the result in the destination operand.
    - **Example**: `ADD EAX, EBX`  
      Adds the value in `EBX` to `EAX`, storing the result in `EAX`.

2. **SUB** (Subtraction)
    - **Description**: Subtracts the second operand from the first operand and stores the result in the destination operand.
    - **Example**: `SUB EAX, EBX`  
      Subtracts the value in `EBX` from `EAX` and stores the result in `EAX`.

3. **MUL** (Unsigned Multiplication)
    - **Description**: Multiplies the accumulator register (`EAX`) by the operand, storing the result in `EDX:EAX`.
    - **Example**: `MUL EBX`  
      Multiplies the value in `EAX` by `EBX`, storing the result in `EDX:EAX`.

4. **IMUL** (Signed Multiplication)
    - **Description**: Multiplies the accumulator register (`EAX`) by the operand, storing the result in `EDX:EAX` (signed).
    - **Example**: `IMUL EAX, EBX`  
      Multiplies the value in `EAX` by `EBX`, storing the result in `EDX:EAX`.

5. **DIV** (Unsigned Division)
    - **Description**: Divides the value in the accumulator register (`EDX:EAX`) by the operand, storing the quotient in `EAX` and the remainder in `EDX`.
    - **Example**: `DIV EBX`  
      Divides the value in `EDX:EAX` by `EBX`, storing the quotient in `EAX` and the remainder in `EDX`.

6. **IDIV** (Signed Division)
    - **Description**: Divides the value in the accumulator register (`EDX:EAX`) by the operand (signed division), storing the quotient in `EAX` and the remainder in `EDX`.
    - **Example**: `IDIV EBX`  
      Divides the value in `EDX:EAX` by `EBX`, storing the quotient in `EAX` and the remainder in `EDX`.

7. **INC** (Increment)
    - **Description**: Increments the operand by 1.
    - **Example**: `INC EAX`  
      Increments the value in `EAX` by 1.

8. **DEC** (Decrement)
    - **Description**: Decrements the operand by 1.
    - **Example**: `DEC EAX`  
      Decrements the value in `EAX` by 1.

9. **AND** (Bitwise AND)
    - **Description**: Performs a bitwise AND between two operands and stores the result in the destination operand.
    - **Example**: `AND EAX, EBX`  
      Performs a bitwise AND between `EAX` and `EBX`, storing the result in `EAX`.

10. **OR** (Bitwise OR)
    - **Description**: Performs a bitwise OR between two operands and stores the result in the destination operand.
    - **Example**: `OR EAX, EBX`  
      Performs a bitwise OR between `EAX` and `EBX`, storing the result in `EAX`.

11. **XOR** (Bitwise XOR)
    - **Description**: Performs a bitwise XOR between two operands and stores the result in the destination operand.
    - **Example**: `XOR EAX, EBX`  
      Performs a bitwise XOR between `EAX` and `EBX`, storing the result in `EAX`.

12. **NOT** (Bitwise NOT)
    - **Description**: Performs a bitwise NOT (inversion) of the operand.
    - **Example**: `NOT EAX`  
      Performs a bitwise NOT on `EAX`, inverting all bits.

13. **NEG** (Negate)
    - **Description**: Negates the operand (computes the two's complement).
    - **Example**: `NEG EAX`  
      Negates the value in `EAX`.

---

## Shift and Rotate Instructions:
1. **SHL** (Shift Left)
    - **Description**: Shifts the bits of the operand to the left, inserting zeros into the least significant bits.
    - **Example**: `SHL EAX, 1`  
      Shifts the bits of `EAX` to the left by 1, filling with zeros.

2. **SHR** (Shift Right)
    - **Description**: Shifts the bits of the operand to the right, inserting zeros into the most significant bits.
    - **Example**: `SHR EAX, 1`  
      Shifts the bits of `EAX` to the right by 1, filling with zeros.

3. **SAR** (Arithmetic Shift Right)
    - **Description**: Shifts the bits of the operand to the right, preserving the sign bit (for signed integers).
    - **Example**: `SAR EAX, 1`  
      Shifts the bits of `EAX` to the right by 1, preserving the sign bit.

4. **ROL** (Rotate Left)
    - **Description**: Rotates the bits of the operand to the left.
    - **Example**: `ROL EAX, 1`  
      Rotates the bits of `EAX` to the left by 1.

5. **ROR** (Rotate Right)
    - **Description**: Rotates the bits of the operand to the right.
    - **Example**: `ROR EAX, 1`  
      Rotates the bits of `EAX` to the right by 1.

---

## Load and Store Instructions:
1. **MOV** (Move)
    - **Description**: Copies data from one operand to another.
    - **Example**: `MOV EAX, EBX`  
      Copies the value in `EBX` to `EAX`.

2. **PUSH** (Push onto stack)
    - **Description**: Pushes a value onto the stack.
    - **Example**: `PUSH EAX`  
      Pushes the value in `EAX` onto the stack.

3. **POP** (Pop from stack)
    - **Description**: Pops a value from the stack into a register.
    - **Example**: `POP EAX`  
      Pops the top value from the stack into `EAX`.

4. **LEA** (Load Effective Address)
    - **Description**: Loads the effective address of a memory operand into a register.
    - **Example**: `LEA EAX, [EBX + ECX*4]`  
      Loads the address calculated from `EBX + ECX*4` into `EAX`.

5. **MOVZX** (Move with Zero Extension)
    - **Description**: Moves a value and zero-extends it to a larger size.
    - **Example**: `MOVZX EAX, BYTE [EBX]`  
      Moves the byte at the memory address in `EBX` into `EAX`, zero-extending it.

6. **MOVSX** (Move with Sign Extension)
    - **Description**: Moves a value and sign-extends it to a larger size.
    - **Example**: `MOVSX EAX, BYTE [EBX]`  
      Moves the byte at the memory address in `EBX` into `EAX`, sign-extending it.

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
    - **Example**: `CMP EAX, EBX`  
      Compares the values in `EAX` and `EBX`.

2. **TEST** (Test)
    - **Description**: Performs a bitwise AND between two operands and updates the flags.
    - **Example**: `TEST EAX, EBX`  
      Performs a bitwise AND between `EAX` and `EBX` and updates the flags.

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

This list covers many of the essential x86 instructions, including those for arithmetic, logic, shifting, branching, stack management, system calls, and more.