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
Interrogate avr example (i.e. check wiring is good):
```shell
$ avrdude -p m328p -c usbasp
```
Communicate with AVR via serial/USART:
```shell
$ screen /dev/ttyUSB0 9600
```
