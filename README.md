# Lab 2: AXI GPIO

## Overview
This lab assignment introduces Block Design in Vivado for utilizing the available AXI GPIO IP to control the 4 LEDs and RGB LED with 4 switch inputs on the Zybo Z7 development board.  Vitis was then used for implementing the control algorithm on the board's processor with a custom C program and applicable libraries.

## Design Summary
Vivado Blocks
- Zynq Processor
- AXI GPIO: LED (4 bits)
- AXI GPIO: RGB LED
- AXI GPIO: Switches (4 bits)

Links between blocks were automatically generated in Vivado before validating the design and generating an XSA file for importing to Vitis.  There, a high level program was written to relate the LED outputs to switch input combinations.  The design followed the truth table below:

|  SW3  |  SW2  |  SW1  |  SW0  |  LED3 |  LED2 |  LED1 |  LED0 |  RGB2  |  RGB1  |  RGB0  |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |  :---: |  :---: |  :---: |
|   0   |   0   |   0   |   0   |   0   |   0   |   0   |   0   |    0   |    0   |    0   |
|   0   |   0   |   0   |   1   |   0   |   0   |   0   |   0   |    1   |    0   |    0   |
|   0   |   0   |   1   |   0   |   0   |   0   |   0   |   0   |    0   |    1   |    0   |
|   0   |   1   |   0   |   0   |   0   |   0   |   0   |   0   |    0   |    0   |    1   |
|   1   |   0   |   0   |   0   |   0   |   0   |   0   |   0   |    1   |    1   |    1   |
|   0   |   0   |   1   |   1   |   bin ctr   |   bin ctr   |   bin ctr   |   bin ctr   |    0   |    0   |    0   |
|   1   |   1   |   0   |   0   |   ring ctr   |   ring ctr   |   ring ctr   |   ring ctr   |    0   |    0   |    0   |

where "bin ctr" suggests the 4 LEDs display a 4-bit binary counter up to 15, and "ring ctr" suggests the LEDs display a ring counter where the output shifts left and cycles over after the 4th bit.  For all other switch combinations not specified, all LEDs + RGB LED remain off.

## Verification and Results
Test Cases for this lab are as described in the truth table in the previous section.  All functionality was verified with hardware implementation.  However, printing to the Vitis console was utilized to verify switch inputs were being read properly when changed.

## Known Issues and Limitations
The challenge here was learning the workflow between Vivado hardware level design and progressing to Vitis for programming the processor in C.  Additionally, it was important to understand how to properly interface with the hardware using the appropriate header files and library definitions.  However, once I discovered how to reference each GPIO defined in Vivado, the C algorithm was fairly straight forward.

## References
Only the lab instructions were used as guidance for this assignment.
