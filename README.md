# stm32_bl

Simple serial bootloader client for STM32 written in bash.

This is a straight forward implementation of the description of the STM32 bootloader protocol in [AN3155](https://www.st.com/resource/en/application_note/cd00264342-usart-protocol-used-in-the-stm32-bootloader-stmicroelectronics.pdf).


Currently only device-IDs from RM0090 and RM0091 (F0 and F4 devices) are recognised, but this is trivially extended.

The main program is 'bl'. By default, it issues the GET command, which makes the chip show what it understands.
After a reset, use the -a option for the first invocation of 'bl' to do autobaud.

The program is not an example of user-friendlyness, but rather follows the AN3155 accurately. The user can create a wrapper script that bundles his typical use-flow, like erase, then write flash. For each bootloader function, call 'bl' once.

The serial port is hardcoded to /dev/ttyUSB0.

# Usage

I have noticed that 'fresh' devices firt must be unprotected both for read (RDU) and write (WPU) before they can be programmed. If they are protected, then the erase (ER or EER) and write (WM) will respond ACK then NACK. Once unprotected, they don't need to be unprotected again.
