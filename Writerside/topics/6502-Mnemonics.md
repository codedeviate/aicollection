# 6502 Mnemonics

The **6502** microprocessor is a popular 8-bit CPU that was widely used in early home computers and video game consoles. It has a relatively simple instruction set, but it is very powerful for its time. Below is a detailed list of the main instructions for the 6502, with explanations, examples, and usage for each.

## Data Processing Instructions:
1. **ADC** (Add with Carry)
    - **Description**: Adds the operand and the carry flag to the accumulator.
    - **Example**: `ADC #$10`  
      Adds the immediate value `$10` and the carry flag to the accumulator.

2. **SBC** (Subtract with Borrow)
    - **Description**: Subtracts the operand and the carry flag from the accumulator (this is effectively a signed subtraction).
    - **Example**: `SBC #$10`  
      Subtracts the immediate value `$10` and the carry flag from the accumulator.

3. **AND** (Logical AND)
    - **Description**: Performs a bitwise AND between the accumulator and the operand.
    - **Example**: `AND #$FF`  
      Performs a bitwise AND between the accumulator and the immediate value `$FF`.

4. **ORA** (Logical OR)
    - **Description**: Performs a bitwise OR between the accumulator and the operand.
    - **Example**: `ORA #$FF`  
      Performs a bitwise OR between the accumulator and the immediate value `$FF`.

5. **EOR** (Exclusive OR)
    - **Description**: Performs a bitwise XOR between the accumulator and the operand.
    - **Example**: `EOR #$FF`  
      Performs a bitwise XOR between the accumulator and the immediate value `$FF`.

6. **CMP** (Compare)
    - **Description**: Compares the accumulator with the operand by subtracting the operand from the accumulator.
    - **Example**: `CMP #$10`  
      Compares the accumulator with the immediate value `$10`.

7. **CPX** (Compare X Register)
    - **Description**: Compares the X register with the operand.
    - **Example**: `CPX #$10`  
      Compares the X register with the immediate value `$10`.

8. **CPY** (Compare Y Register)
    - **Description**: Compares the Y register with the operand.
    - **Example**: `CPY #$10`  
      Compares the Y register with the immediate value `$10`.

9. **BIT** (Bit Test)
    - **Description**: Tests specific bits of the accumulator with the operand.
    - **Example**: `BIT $2000`  
      Tests the bits of the accumulator against the memory at address `$2000`.

---

## Load and Store Instructions:
1. **LDA** (Load Accumulator)
    - **Description**: Loads a value into the accumulator.
    - **Example**: `LDA #$10`  
      Loads the immediate value `$10` into the accumulator.

2. **LDX** (Load X Register)
    - **Description**: Loads a value into the X register.
    - **Example**: `LDX #$10`  
      Loads the immediate value `$10` into the X register.

3. **LDY** (Load Y Register)
    - **Description**: Loads a value into the Y register.
    - **Example**: `LDY #$10`  
      Loads the immediate value `$10` into the Y register.

4. **STA** (Store Accumulator)
    - **Description**: Stores the value in the accumulator into memory.
    - **Example**: `STA $2000`  
      Stores the value in the accumulator into memory at address `$2000`.

5. **STX** (Store X Register)
    - **Description**: Stores the value in the X register into memory.
    - **Example**: `STX $2000`  
      Stores the value in the X register into memory at address `$2000`.

6. **STY** (Store Y Register)
    - **Description**: Stores the value in the Y register into memory.
    - **Example**: `STY $2000`  
      Stores the value in the Y register into memory at address `$2000`.

7. **TAX** (Transfer Accumulator to X)
    - **Description**: Transfers the value in the accumulator to the X register.
    - **Example**: `TAX`  
      Copies the value from the accumulator into the X register.

8. **TAY** (Transfer Accumulator to Y)
    - **Description**: Transfers the value in the accumulator to the Y register.
    - **Example**: `TAY`  
      Copies the value from the accumulator into the Y register.

9. **TXA** (Transfer X to Accumulator)
    - **Description**: Transfers the value in the X register to the accumulator.
    - **Example**: `TXA`  
      Copies the value from the X register into the accumulator.

10. **TYA** (Transfer Y to Accumulator)
    - **Description**: Transfers the value in the Y register to the accumulator.
    - **Example**: `TYA`  
      Copies the value from the Y register into the accumulator.

11. **TXS** (Transfer X to Stack Pointer)
    - **Description**: Transfers the value in the X register to the stack pointer.
    - **Example**: `TXS`  
      Copies the value from the X register into the stack pointer.

---

## Stack Instructions:
1. **PHA** (Push Accumulator)
    - **Description**: Pushes the value in the accumulator onto the stack.
    - **Example**: `PHA`  
      Pushes the value in the accumulator onto the stack.

2. **PHP** (Push Processor Status)
    - **Description**: Pushes the processor status (flags) onto the stack.
    - **Example**: `PHP`  
      Pushes the processor status register onto the stack.

3. **PLA** (Pull Accumulator)
    - **Description**: Pulls a value from the stack into the accumulator.
    - **Example**: `PLA`  
      Pulls a value from the stack into the accumulator.

4. **PLP** (Pull Processor Status)
    - **Description**: Pulls a value from the stack into the processor status register.
    - **Example**: `PLP`  
      Pulls a value from the stack into the processor status register.

---

## Branch Instructions:
1. **JMP** (Jump)
    - **Description**: Unconditionally jumps to the specified memory address.
    - **Example**: `JMP $2000`  
      Jumps to the address `$2000`.

2. **JSR** (Jump to Subroutine)
    - **Description**: Jumps to a subroutine and pushes the return address onto the stack.
    - **Example**: `JSR $2000`  
      Jumps to the address `$2000` and pushes the return address onto the stack.

3. **RTS** (Return from Subroutine)
    - **Description**: Returns from a subroutine by pulling the return address from the stack.
    - **Example**: `RTS`  
      Returns from the subroutine by pulling the return address from the stack.

4. **BEQ** (Branch if Equal)
    - **Description**: Branches if the zero flag is set.
    - **Example**: `BEQ label`  
      Branches to the label if the zero flag is set (i.e., if the last operation resulted in zero).

5. **BNE** (Branch if Not Equal)
    - **Description**: Branches if the zero flag is clear.
    - **Example**: `BNE label`  
      Branches to the label if the zero flag is clear (i.e., if the last operation did not result in zero).

6. **BCC** (Branch if Carry Clear)
    - **Description**: Branches if the carry flag is clear.
    - **Example**: `BCC label`  
      Branches to the label if the carry flag is clear.

7. **BCS** (Branch if Carry Set)
    - **Description**: Branches if the carry flag is set.
    - **Example**: `BCS label`  
      Branches to the label if the carry flag is set.

8. **BMI** (Branch if Minus)
    - **Description**: Branches if the negative flag is set (i.e., the result of the last operation was negative).
    - **Example**: `BMI label`  
      Branches to the label if the negative flag is set.

9. **BPL** (Branch if Positive)
    - **Description**: Branches if the negative flag is clear (i.e., the result of the last operation was positive).
    - **Example**: `BPL label`  
      Branches to the label if the negative flag is clear.

---

## Miscellaneous Instructions:
1. **NOP** (No Operation)
    - **Description**: Does nothing; typically used for padding or timing purposes.
    - **Example**: `NOP`  
      Does nothing and proceeds to the next instruction.

2. **SEC** (Set Carry Flag)
    - **Description**: Sets the carry flag.
    - **Example**: `SEC`  
      Sets the carry flag.

3. **CLC** (Clear Carry Flag)
    - **Description**: Clears the carry flag.
    - **Example**: `CLC`  
      Clears the carry flag.

4. **SED** (Set Decimal Flag)
    - **Description**: Sets the decimal mode flag, which affects the BCD (Binary-Coded Decimal) operations.
    - **Example**: `SED`  
      Sets the decimal mode flag.

5. **CLD** (Clear Decimal Flag)
    - **Description**: Clears the decimal mode flag.
    - **Example**: `CLD`  
      Clears the decimal mode flag.

6. **SEI** (Set Interrupt Disable)
    - **Description**: Sets the interrupt disable flag.
    - **Example**: `SEI`  
      Sets the interrupt disable flag.

7. **CLI** (Clear Interrupt Disable)
    - **Description**: Clears the interrupt disable flag.
    - **Example**: `CLI`  
      Clears the interrupt disable flag.

8. **BRK** (Break)
    - **Description**: Triggers an interrupt, causing the processor to stop executing the current instruction and begin an interrupt service routine.
    - **Example**: `BRK`  
      Triggers a break interrupt.

---

This list covers the most important and commonly used instructions in the **6502** processor architecture, including arithmetic, logic, branching, memory operations, stack management, and more. The simplicity of the instruction set made the 6502 a very efficient processor for its time, widely used in gaming consoles, early personal computers, and embedded systems.