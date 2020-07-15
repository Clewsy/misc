# Conky stuff
To get temperature sensos working, install lm-sensors
```shell
$ sudo apt update && sudo apt install lm-sensors
```

Run it to figure out the host's sensors:
```shell
$ sudo sensors-detect
$ sudo service module-init-tools restart
```

test it:
```shell
$ sensors
```
