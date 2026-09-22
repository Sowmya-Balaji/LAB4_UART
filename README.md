FINITE STATE MACHINE TO CHANGE LED COLOUR AND BLINK SPEED USING SWITCH AND UART CONTROL

Sowmya Balaji, SR no. 28488

Electronic Systems Engineering, IISc

1. Objective

The objective of this assignment is to extend the finite state machine developed in Lab 3 so that the global state of the machine—comprising Status (Running/Paused), Colour, and Blink Speed—can be controlled not only through onboard switches but also through commands entered on a UART console. The RGB LED and 4-digit multiplexed 7-segment display continue to reflect the current global state regardless of which input source triggered the change.

2. Hardware & GPIO Configuration

The experiment utilizes the TM4C123GH6PM LaunchPad and the EduARM4 addon board. Onboard switches SW1 (PF4) and SW2 (PF0) remain configured as inputs to detect user button presses. In addition, UART0 is configured to communicate with a PC terminal over the USB-to-serial connection, allowing the user to type commands into a serial console. The microcontroller's outputs continue to drive the RGB LED and the 4-digit multiplexed 7-segment display on the addon board.

3. State Machine Design & Switch + UART Control

The program retains the global finite state machine from Lab 3 to manage the active status, LED colour, and blink speed, and extends it so that the same state variables can be updated from either the switches or the UART console. Proper switch debouncing and UART command parsing are both implemented to guarantee accurate, glitch-free state transitions.

●	Running State (Switches): Pressing SW1 increments the LED blink speed level, cycling through levels S1 to S8. Pressing SW2 cycles the LED through seven possible colours (primary RGB and their combinations). Selecting colour code zero completely switches off all the LEDs.

●	Running State (UART Console): Typing 'rate' into the console increments the LED blink speed level, cycling through S1 to S8, identically to a SW1 press. Typing 'color' into the console cycles the LED colour through the same seven colours (and off state) used by SW2.

●	Paused State: Pressing both SW1 and SW2 simultaneously, or typing 'pause' into the console, transitions the machine into a paused state. During this state, the machine holds its current colour continuously without blinking.

●	Resuming: Pressing both switches again, or typing 'run' into the console, releases the paused state, returning the machine to standard running operation.

4. 7-Segment Display Output

The program continuously maps the internal global state—however it was last updated—to the 4-digit 7-segment display. The display multiplexing is programmed to ensure a flicker-free visual output during both the Running and Paused states, regardless of whether the last change came from a switch press or a UART command. The four modules display the following data:

●	Module 1: Displays the overall Status ('r' for Running, 'P' for Paused).

●	Module 2: Displays the current colour code of the machine (1...7, 0).

●	Modules 3 & 4: Display the current blink speed level (S1...S8).

5. Conclusion

This assignment successfully extended the finite state machine from Lab 3 to accept commands from two independent input sources—onboard switches and a UART console—while sharing a single global state. By merging switch debouncing with UART command parsing ('rate', 'color', 'pause', 'run'), the program maintained consistent colour, blink speed, and pause/run behaviour, while sustaining a stable, flicker-free multiplexed 7-segment display.
