# DefCon29Badge

Here's my dump of the DC29 badge.  I used a Bus Blaster v2 with the KT-Link buffer loaded on it to interface with the badge using OpenOCD and GDB.  The config file to connect to the badge is openocd-samd21.cfg.

You will need to connect to via SWD on the tag connect port. Looking at the connector with the single alignment hole on the left, the pin ordering starts with pin 1 on the bottom left and goes anti-clockwise to 10. (pin numbering can be seen on https://www.tag-connect.com/wp-content/uploads/bsk-pdf-manager/TC2050-IDC_Datasheet_7.pdf)

The following connections are used
Pin 1 - VCC (3.1v DC is what I measured on my badge)
Pin 2 - SWDIO
Pin 3 - GND
Pin 4 - SWDCLK

To connect with OpenOCD, run the command:
openocd -f openocd-samd21.cfg

This will open up a GDB session on port 3333 by default.  You can connect to it with the ARM GDB util:
arm-none-eabi-gdb

Issue the following commands to get your firmware dump:
target extended-remote 127.0.0.1:3333
dump binary memory dc29-human.bin 0x0 0xFFFF


