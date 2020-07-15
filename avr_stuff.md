# install avrdude stuff
```shell
$ sudo apt-get install avrdude avrdude-doc binutils-avr avr-libc gcc-avr gdb-avr
```

# making - will compile executable "main"
from command line:
```shell
$ gcc main.c another_file.c serialLibrary.c -o main
```

or from a makefile, first:
```shell
main: main.c another_file.c serialLibrary.c
```
then make with command:
```shell
$ make main
```

# avrdude stuff
list all compatible packages:
```shell
$ avrdude -p ?
```
list all programmers:
```shell
$ avrdude -c ?
```
interrogate avr example (i.e. check wiring is all good):
```shell
$ avrdude -p m328p -c usbasp
```
communicate with AVR via serial/USART:
```shell
$ screen /dev/ttyUSB0 9600
```