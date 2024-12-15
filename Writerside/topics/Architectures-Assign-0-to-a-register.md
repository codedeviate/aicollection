# Assign 0 to a register

The fastest way to set a register to 0 in different processor architectures is typically to XOR the register with itself. This is because the XOR operation is generally very fast and does not require loading an immediate value. Here are examples for different architectures:

## x86/x64
```nasm
xor eax, eax  ; Set eax to 0
```

## ARM
```nasm
eor x0, x0, x0  ; Set x0 to 0
```

## MIPS
```nasm
xor $t0, $t0, $t0  ; Set $t0 to 0
```

## PowerPC
```nasm
xor r0, r0, r0  ; Set r0 to 0
```

Using XOR with itself is a common and efficient way to zero a register across various architectures.