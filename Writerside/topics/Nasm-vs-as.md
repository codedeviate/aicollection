# Nasm vs as

`nasm` (Netwide Assembler) and `as` (GNU Assembler) are two different assemblers for x86 and x86-64 assembly language, and they have different syntax and conventions.

## Key Differences:

1. **Section and Global Directives**:
    - `nasm` uses `.section .text` and `.global _start`.
    - `as` uses `section .text` and `global _start`.

2. **Register and Instruction Syntax**:
    - `nasm` uses `%` prefix for registers and `$` for immediate values.
    - `as` does not use `%` for registers and uses `$` for immediate values.

3. **Comment Syntax**:
    - `nasm` uses `;` for comments.
    - `as` uses `#` for comments.

## Flags:

### `nasm` Flags:

- `elf32` or `elf64`: Specifies the output format as 32-bit or 64-bit ELF.

## Example:

### `nasm` Syntax:
```nasm
section .text
global _start

_start:
    mov rax, 60         ; Syscall number for exit
    xor rdi, rdi        ; Exit code 0
    syscall             ; Invoke the syscall
```

### `as` Syntax:
```nasm
.section .text
.global _start

_start:
    mov $60, %rax       # Syscall number for exit
    xor %rdi, %rdi      # Exit code 0
    syscall             # Invoke the syscall
```

These differences are due to the design choices and conventions adopted by the developers of each assembler.