# PIC

## History
The PIC (Peripheral Interface Controller) is a family of microcontrollers made by Microchip Technology. It was first introduced in 1976 and has been widely used in various embedded applications. The PIC microcontrollers are known for their ease of use, low cost, and wide range of available peripherals.

## Features
- **8-bit, 16-bit, and 32-bit architectures**: Available in different configurations to suit various applications.
- **Harvard architecture**: Separate memory spaces for instructions and data, allowing simultaneous access to both.
- **Peripheral support**: Includes a wide range of peripherals like timers, UART, SPI, and I2C.
- **Low power consumption**: Suitable for battery-powered applications.
- **In-system programmable**: Allows for easy updates and modifications to the firmware.

## Example Code
Here is a simple PIC C program to blink an LED:

```c
#include <xc.h>

void main(void) {
    TRISBbits.TRISB0 = 0; // Set RB0 as output
    while (1) {
        LATBbits.LATB0 = ~LATBbits.LATB0; // Toggle RB0
        __delay_ms(500); // Delay for 500 ms
    }
}
```

This code configures the PIC microcontroller to toggle an LED connected to pin RB0 with a delay, creating a blinking effect.