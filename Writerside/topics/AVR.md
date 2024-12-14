# AVR

## History
The AVR is a family of microcontrollers developed by Atmel (now part of Microchip Technology) in 1996. It is widely used in embedded systems, particularly in hobbyist and educational projects, such as Arduino.

## Features
- **8-bit architecture**: Processes 8 bits of data at a time.
- **RISC architecture**: Reduced Instruction Set Computing for efficient performance.
- **Flash memory**: In-system programmable flash memory for code storage.
- **Peripheral support**: Includes various peripherals like timers, ADCs, and communication interfaces.

## Example Code
Here is a simple AVR C program to blink an LED:

```c
#include <avr/io.h>
#include <util/delay.h>

int main(void) {
    DDRB |= (1 << PB0); // Set PB0 as output
    while (1) {
        PORTB ^= (1 << PB0); // Toggle PB0
        _delay_ms(500); // Delay for 500 ms
    }
    return 0;
}
```

This code configures the AVR microcontroller to toggle an LED connected to pin PB0 with a delay, creating a blinking effect.