# Beaglebone Black setup.

To flash eMMC, after dd'ing image to sd card, enable flasher.  Remove #comment symbol:
```shell
$ vim /media/user/rootfs/boot/uEnv.txt
```
Change:
```shell
#cmdline=init=/opt/scripts/tools/eMMC/init-eMMC-flasher-v3.sh
```
to:
```shell
cmdline=init=/opt/scripts/tools/eMMC/init-eMMC-flasher-v3.sh
```

Optionally, update the flasher scripts:
```shell
$ cd /media/user/rootfs/opt/scripts
$ git pull
```

Reboot and system will be flashed automatically.  Remember to remove sd card else it will keep re-flashing.  All four LEDs will act as a larson scanner while flashing and will turn off once complete.

Default login is debian:temppwd
