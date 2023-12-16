# Install avrdude stuff
```shell
$ sudo apt update && sudo apt install \
    avrdude \
    avrdude-doc \
    binutils-avr \
    avr-libc \
    gcc-avr \
    gdb-avr
```

# Making - will compile executable "main"
1. Direct from command line:
```shell
$ gcc main.c another_file.c serialLibrary.c -o main
```

2. From a makefile, first:
```shell
main: main.c another_file.c serialLibrary.c
```
Then make with command:
```shell
$ make main
```

# avrdude stuff
List all compatible packages:
```shell
$ avrdude -p ?
```
List all programmers:
```shell
$ avrdude -c ?
```
Interrogate avr example (i.e. check wiring is good)  Also shows fuse byte values:
```shell
$ avrdude -p m328p -c usbasp #no need to specify port for usbasp.
$ avrdude -p m328p -c stk500v2 -P /dev/ttyACM0  #need to specify port for stk500v2.
```
Communicate with AVR via serial/USART:
```shell
$ screen /dev/ttyUSB0 9600
```

Write fuse bits:
```shell
$ avrdude -p m328p -c usbasp -U hfuse:w:0xD9:m
```
Fuse bytes are low (lfuse) high (hfuse) and extended (efuse).
Link to useful fuse info: http://eleccelerator.com/fusecalc/fusecalc.php?chip=atmega32u4
Don't forget the avrdude manual: https://www.nongnu.org/avrdude/user-manual/avrdude_toc.html#SEC_Contents

Directly write a hex file to an AVR:
```shell
$ avrdude -p m32u4 -c stk500v2 -P /dev/ttyACM0 -U flash:w:Caterina-Leonardo.hex:i
```

Directly download a hex file from an AVR:
```shell
$ avrdude -p m32u4 -c stk500v2 -P /dev/ttyACM0 -U flash:r:Caterina-Leonardo.hex:i
```

