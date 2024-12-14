# 68XX Embedded

## History
The 68XX family of microprocessors, developed by Motorola, includes several 8-bit microcontrollers widely used in embedded systems. The family started with the 6800, introduced in 1974, and expanded to include various derivatives like the 6801, 6803, and 68HC11, each offering enhancements and additional features.

## Features
- **8-bit architecture**: Processes 8 bits of data at a time.
- **Harvard architecture**: Separate memory spaces for instructions and data in some variants.
- **Peripheral support**: Includes a variety of peripherals like timers, serial communication interfaces, and ADCs.
- **Low power consumption**: Suitable for battery-powered applications.
- **In-system programmable**: Allows for easy updates and modifications to the firmware.

## Example Code
Here is a simple 68HC11 assembly program to blink an LED:

```nasm
    ORG $1000
    LDX #$1000        ; Load index register X with the address of the data direction register
    LDAA #$01         ; Load accumulator A with the value 1
    STAA $1004        ; Store the value in the data direction register to set pin as output
loop:
    COMA             ; Complement the value in accumulator A (toggle)
    STAA $1005       ; Store the value in the port register to toggle the LED
    JSR DELAY        ; Call delay subroutine
    BRA loop         ; Branch to loop
DELAY:
    LDX #$FFFF       ; Load index register X with a delay value
delay_loop:
    DEX              ; Decrement index register X
    BNE delay_loop   ; Branch if not equal to zero
    RTS              ; Return from subroutine
```

This code configures the 68HC11 microcontroller to toggle an LED connected to a specific port with a delay, creating a blinking effect.