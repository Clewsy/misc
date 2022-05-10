# Setting time and date

## Set system time
```shell
$ sudo date -s 11:37:30
```

## Set system date
```shell
$ sudo date -s 22-05-10
```

## Set hardware clock time from system time
```shell
$ sudo hwclock --systohc
```

## Set system time from hardware clock
```shell
$ sudo hwclock --hctosys
```

## Enable ntp server sync.
```shell
$ sudo timedatectl set-ntp on
```

## Change timezone
```shell
$ sudo timedatectl set-timezone Antarctica/Casey
```

