# Arm and Aarch64

## History of the ARM Architecture

### 1. **Early Development (1980s)**
- **Acorn Computers**: ARM (originally Acorn RISC Machine) was developed by Acorn Computers in the 1980s. The first ARM processor, the ARM1, was designed in 1985.
- **ARM2**: The ARM2, released in 1986, was the first widely used ARM processor, featuring a 32-bit data bus and a 26-bit address space.

### 2. **Formation of ARM Ltd. (1990)**
- **Joint Venture**: In 1990, Acorn Computers, Apple, and VLSI Technology formed a joint venture called Advanced RISC Machines Ltd. (ARM Ltd.) to further develop and license the ARM architecture.

### 3. **ARM7 and ARM9 (1990s)**
- **ARM7**: The ARM7 series, introduced in the early 1990s, became one of the most successful ARM cores, widely used in embedded systems.
- **ARM9**: The ARM9 series, introduced in the late 1990s, offered improved performance and power efficiency, making it popular in mobile devices.

### 4. **ARM11 and Cortex Series (2000s)**
- **ARM11**: The ARM11 series, introduced in the early 2000s, was used in many early smartphones, including the first iPhone.
- **Cortex-A, Cortex-R, Cortex-M**: ARM introduced the Cortex series, with Cortex-A for high-performance applications, Cortex-R for real-time applications, and Cortex-M for microcontrollers.

### 5. **ARMv8 and 64-bit Architecture (2011)**
- **ARMv8-A**: In 2011, ARM introduced the ARMv8-A architecture, which added 64-bit support (AArch64) alongside the existing 32-bit support (AArch32).
- **Adoption**: ARMv8-A was quickly adopted in smartphones, tablets, and servers, with notable implementations like Apple's A7 chip and AWS Graviton processors.

### 6. **Recent Developments (2020s)**
- **ARMv9**: In 2021, ARM announced the ARMv9 architecture, focusing on enhanced security, AI, and machine learning capabilities.
- **Apple Silicon**: Apple transitioned its Mac computers to ARM-based processors with the introduction of the M1 chip in 2020, followed by the M1 Pro, M1 Max, and M2 chips.

### Summary
ARM architecture has evolved from its origins in the 1980s to become a dominant force in mobile and embedded computing, with recent advancements pushing it into high-performance computing and server markets.

## Technical Comparison: ARM (AArch32) vs. AArch64 (64-bit ARM)
Here's a **detailed technical comparison** between ARM (AArch32) and AArch64:

### 1. **Architecture Versions and Modes**
| Feature                  | ARM (AArch32)                | AArch64 (64-bit ARM)                                                       |
|--------------------------|------------------------------|----------------------------------------------------------------------------|
| **Architecture Version** | ARMv7 (32-bit) and earlier   | ARMv8 and later                                                            |
| **Execution Mode**       | AArch32 (32-bit)             | AArch64 (64-bit)                                                           |
| **Instruction Set**      | ARM, Thumb, and Thumb-2      | A64 (64-bit instruction set)                                               |
| **Compatibility**        | Can execute only 32-bit code | Can execute both 32-bit (AArch32) and 64-bit (AArch64) code on ARMv8+ CPUs |

### 2. **Instruction Set Differences**
| Feature              | ARM (AArch32)                       | AArch64                                                               |
|----------------------|-------------------------------------|-----------------------------------------------------------------------|
| **Instruction Size** | Mostly 32-bit (ARM), 16-bit (Thumb) | Fixed 32-bit instruction width                                        |
| **New Instructions** | Limited to ARMv7 extensions         | New atomic, cryptographic, and SIMD instructions (e.g., `LDP`, `STP`) |
| **Floating Point**   | VFPv3 or NEON optional              | Integrated NEON and floating-point as standard                        |
| **SIMD Extensions**  | Separate NEON (32 registers)        | Unified SIMD and floating-point registers (128-bit wide)              |

### 3. **Registers**
| Feature                       | ARM (AArch32)                 | AArch64                                        |
|-------------------------------|-------------------------------|------------------------------------------------|
| **General Purpose Registers** | 16 registers (R0–R15, 32-bit) | 31 registers (X0–X30, 64-bit)                  |
| **Special Registers**         | PC (R15), LR (R14), SP (R13)  | PC (Program Counter), SP, LR (X30)             |
| **Zero Register**             | No dedicated zero register    | XZR/WZR as a zero register                     |
| **Stack Pointer**             | Single stack pointer (SP)     | Separate SP_ELx for different execution levels |

### 4. **Memory Addressing**
| Feature                   | ARM (AArch32)                          | AArch64                                  |
|---------------------------|-----------------------------------------|------------------------------------------|
| **Address Space**          | 4 GB (32-bit addressing)               | 16 EB (theoretical, limited to 48-bit/57-bit implementations) |
| **Memory Model**           | Little-endian or big-endian            | Primarily little-endian, optional big-endian |
| **Addressing Modes**       | Variety of complex addressing modes    | Simplified addressing modes for efficiency |

### 5. **Operating Modes and Exception Levels**
| Feature              | ARM (AArch32)                            | AArch64                                                          |
|----------------------|------------------------------------------|------------------------------------------------------------------|
| **Privileged Modes** | 7 processor modes (User, FIQ, IRQ, etc.) | 4 Exception Levels (EL0 to EL3)                                  |
| **Exception Levels** | None                                     | EL0 (User), EL1 (Kernel), EL2 (Hypervisor), EL3 (Secure Monitor) |
| **Virtualization**   | Minimal support                          | Full hardware virtualization (EL2)                               |

### 6. **Performance and Power**
| Feature              | ARM (AArch32)                    | AArch64                                                                     |
|----------------------|----------------------------------|-----------------------------------------------------------------------------|
| **Power Efficiency** | Optimized for low power          | Maintains power efficiency but supports higher performance                  |
| **Performance**      | Limited due to 32-bit operations | Higher performance due to 64-bit registers, SIMD, and advanced instructions |

### 7. **Use Cases**
| Use Case              | ARM (AArch32)                        | AArch64                                                  |
|-----------------------|--------------------------------------|----------------------------------------------------------|
| **Embedded Systems**  | Widely used in microcontrollers, IoT | Emerging use in advanced embedded systems                |
| **Mobile Devices**    | ARMv7 (older smartphones, tablets)   | Standard in modern smartphones (ARMv8+)                  |
| **Server/Datacenter** | Rare usage                           | Widely used in servers (e.g., AWS Graviton, Apple M1/M2) |
| **Desktops/Laptops**  | Rare usage                           | Increasing use (Apple Silicon, Windows on ARM)           |

### Summary of Key Enhancements in AArch64:
1. **Larger Register Set:** More general-purpose registers (31 vs. 16).
2. **Unified NEON/SIMD:** Single set of registers for SIMD and floating-point operations.
3. **Improved Exception Levels:** Cleaner privilege separation for better security.
4. **64-bit Addressing:** Enables large memory support and better performance for data-intensive applications.
5. **New Instructions:** For cryptography, virtualization, and atomic operations.

### Conclusion
AArch64 is a major leap forward, designed for high performance, larger memory space, and modern computing needs, while maintaining ARM's hallmark efficiency. ARM (AArch32) remains relevant in low-power, constrained environments like IoT and embedded systems.