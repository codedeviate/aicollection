# 68020 Registers

The Motorola 68000 and 68010 processors have very similar register sets. The primary differences between the two are related to enhancements in the 68010 for improved performance and additional features. Here are the key differences:

## 68000 Registers

1. **General Purpose Registers**
    - **D0 - D7 (Data Registers)**
    - **A0 - A7 (Address Registers)**

2. **Stack Pointer**
    - **A7 (User Stack Pointer, USP)**
    - **SSP (Supervisor Stack Pointer)**

3. **Program Counter**
    - **PC (Program Counter)**

4. **Status Register**
    - **SR (Status Register)**

5. **Condition Code Register**
    - **CCR (Condition Code Register)**

## 68010 Registers

The 68010 includes all the registers of the 68000 with the following enhancements:

1. **Vector Base Register (VBR)**
    - Allows relocation of the exception vector table, providing more flexibility in handling exceptions.

2. **Alternate Function Code Registers (SFC and DFC)**
    - **SFC (Source Function Code Register)**
    - **DFC (Destination Function Code Register)**
    - These registers are used to control the function codes for memory access, allowing more sophisticated memory management.

## Summary

- The 68010 includes all the registers of the 68000.
- The 68010 adds the **Vector Base Register (VBR)** for relocating the exception vector table.
- The 68010 introduces **Source Function Code Register (SFC)** and **Destination Function Code Register (DFC)** for advanced memory management.

These enhancements in the 68010 provide improved performance and additional features compared to the 68000.