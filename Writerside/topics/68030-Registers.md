# 68030 Registers

The Motorola 68000 and 68030 processors have several differences in their register sets and capabilities. Here are the key differences:

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

## 68030 Registers

The 68030 includes all the registers of the 68000 with the following enhancements:

1. **Cache Control Registers**
    - **CACR (Cache Control Register)**
    - Used to control the on-chip cache.

2. **Address Space Registers**
    - **ASID (Address Space Identifier)**
    - Used for virtual memory management.

3. **Additional Control Registers**
    - **TC (Translation Control Register)**
    - **TT0, TT1 (Transparent Translation Registers)**
    - Used for memory management and translation.

4. **Vector Base Register (VBR)**
    - Allows relocation of the exception vector table, providing more flexibility in handling exceptions.

5. **Alternate Function Code Registers (SFC and DFC)**
    - **SFC (Source Function Code Register)**
    - **DFC (Destination Function Code Register)**
    - These registers are used to control the function codes for memory access, allowing more sophisticated memory management.

## Summary

- The 68030 includes all the registers of the 68000.
- The 68030 adds **Cache Control Registers (CACR)** for cache management.
- The 68030 introduces **Address Space Identifier (ASID)** for virtual memory management.
- The 68030 includes additional control registers like **Translation Control Register (TC)** and **Transparent Translation Registers (TT0, TT1)** for advanced memory management.
- The 68030 retains the **Vector Base Register (VBR)** and **Source Function Code Register (SFC)** and **Destination Function Code Register (DFC)** from the 68010 for enhanced memory management and exception handling.

These enhancements in the 68030 provide improved performance, advanced memory management, and additional features compared to the 68000.