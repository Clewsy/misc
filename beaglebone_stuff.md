# Beaglebone Black setup.

To flash eMMC, after dd'ing image to sd card, enable flasher.  Remove #comment symbol:
```shell
$ vim /media/user/rootfs/boot/uEnv.txt
```
Change:
```shell
#cmdline=init=/usr/sbin/init-beagle-flasher
```
to:
```shell
cmdline=init=/usr/sbin/init-beagle-flasher
```

Optionally, update the flasher scripts:
(scripts directory no longer present - no longer applicable?)
```shell
$ cd /media/user/rootfs/opt/scripts
$ git pull
```

Reboot and system will be flashed automatically.  Remember to remove sd card else it will keep re-flashing.  All four LEDs will act as a larson scanner while flashing and will turn off once complete.

Default login is debian:temppwd

# Beaglebone Black Wireless Setup

Instructions above are applicable with the addition of the following wifi config:

Unable to configure for automatic connection after first boot :(

Connect via tethered usb:
```shell
$ ssh debian@192.168.6.2
```

Default password is: temppwd

Use connmanctl to configure wifi:
```shell
connmanctl
connmanctl> tether wifi off
connmanctl> enable wifi
connmanctl> scan wifi
connmanctl> services
connmanctl> agent on
connmanctl> connect wifi_*_managed_psk
connmanctl> quit
```
