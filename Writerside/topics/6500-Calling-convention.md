# 6500 Calling convention

The 6500 calling convention is a set of rules that dictate how functions receive parameters and return values, how the stack is managed, and how registers are used. This ensures that code generated by different compilers can interoperate.

## Key Points of the 6500 Calling Convention

1. **Registers**:
    - **General-purpose registers**: A (Accumulator), X, Y.
    - **Stack pointer**: SP.
    - **Program counter**: PC.
    - **Status register**: P.

2. **Parameter Passing**:
    - Parameters are typically passed in memory or via the stack.
    - The caller pushes the arguments onto the stack before calling the function.

3. **Return Values**:
    - The primary return value is placed in the Accumulator (A).

4. **Stack Management**:
    - The stack is managed using the Stack Pointer (SP).
    - The caller is responsible for cleaning up the stack after the function call.

5. **Callee-saved Registers**:
    - The callee must save and restore any registers it uses.

## Example

Here is an example of a simple function in 6500 assembly that adds two integers:

```nasm
    .org $8000
add:
    CLC             ; Clear carry flag
    LDA $00         ; Load first argument from memory
    ADC $01         ; Add second argument with carry
    STA $02         ; Store result in memory
    RTS             ; Return from subroutine
```

## Explanation (1)

- The function `add` takes two integer arguments from memory locations `$00` and `$01`.
- It adds the values, storing the result in memory location `$02`.
- The `RTS` instruction returns to the caller.

## Example with Stack Usage

Here is an example of a function that uses the stack to store local variables:

```nasm
    .org $8000
sum_array:
    PHA             ; Save Accumulator
    TXA             ; Transfer X to A
    PHA             ; Save X
    TYA             ; Transfer Y to A
    PHA             ; Save Y

    LDX #$00        ; Initialize index to 0
    LDA #$00        ; Initialize sum to 0

loop:
    CPX $01         ; Compare index with array length
    BEQ end_loop    ; If index == length, exit loop

    LDA $02, X      ; Load array element
    CLC             ; Clear carry flag
    ADC $03         ; Add to sum
    STA $03         ; Store sum
    INX             ; Increment index
    JMP loop        ; Repeat loop

end_loop:
    PLA             ; Restore Y
    TAY             ; Transfer A to Y
    PLA             ; Restore X
    TAX             ; Transfer A to X
    PLA             ; Restore Accumulator
    RTS             ; Return from subroutine
```

## Explanation (2)

- The function `sum_array` takes two arguments: the array length in memory location `$01` and the array starting at memory location `$02`.
- It saves the Accumulator, X, and Y registers on the stack.
- It initializes the sum and index to 0.
- It enters a loop to iterate over the array, loading each element, adding it to the sum, and incrementing the index.
- After the loop, it restores the registers from the stack and returns.

These examples illustrate the basic principles of the 6500 calling convention, including register usage, parameter passing, and stack management.