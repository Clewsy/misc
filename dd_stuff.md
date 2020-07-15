# dd

## -1.0 Don't forget to unmount first else dd may not work
```shell
$ umount /media/b4t/drive
```

## 0.0 standard example
```shell
$ sudo dd if=/some/file.iso of=/dev/sdX bs=1M
```

## 1.0 use pv (pipe viewer) to get live progress output
```shell
$ sudo dd if=/some/file.iso bs=1M | pv | dd of=/dev/sdX
```

## 2.0 use kill with -USR1 switch to output current progress
```shell
$ sudo dd if=/some/file.iso of=/dev/sdX bs=1M
$ sudo kill -USR1 <pidofddcommand>
```

### 2.1 shell shortcut to get pidofddcommand
```shell
$ sudo kill -USR1 $(pgrep ^dd)
```

## 3.0 use dd embedded progress bar
```shell
$ sudo dd if=/some/file.iso of=/dev/sdX bs=1M status=progress
```
