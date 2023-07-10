# Talk to serial devices

## screen
```shell
#screen examples
$ screen /dev/ttyS0 9600
$ screen /dev/ttyUSB0 1200
```
With different serial protocol.
```shell
#screen example
$ stty -F /dev/ttyUSB0 cs7 parenb parodd -cstopb    #first reconfigure tty port
$ screen /dev/ttyUSB0 1200                          #then connect with screen
```
Where:
- -F : open File <device>
- Character Bits:
    - cs7 : 7 data bits
    - cs8 : 8 data bits
- Parity:
    - parenb  : enable parity bit
    - -parenb : don't enable parity bit
    - parodd  : use odd parity
    - -parodd : use even parity
- Stop bit/s:
    - cstop  : use two stop bits per character
    - -cstop : use just one stop bit per character

To quit screen: "ctrl-a" followed by '/'

## minicom
```shell
$ minicom -s # -s to start with the settings screen (instead of /dev/modem).
```
1. Navigate to "Serial port setup".
2. Select 'A' to change the tty device.
3. Select 'E' to change the baud and serial protocol.
4. Hit enter when done.
5. <Optional> Save config file or save as default.
6. Navigate to and select "Exit".
7. You're now connected to the serial device.

Enter "crtl-A" follwed by 'z' to show help menu.
Enter "ctrl-a" followed by 'q' to quit.
