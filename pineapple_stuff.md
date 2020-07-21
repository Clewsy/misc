# Default web interface ip
172.16.42.1:1471

# Get automated config/connection script
```shell
$ wget https://www.wifipineapple.com/wp6.sh
$ chmod +x wp6.sh
```

# Set up root profile - modify existing profile at /etc/profile
```shell
$ vim /etc/profile
```
Or create new profile file in home directory
```shell
$ vim /root/.profile
```

# SD card mount location is /sd
```shell
cd /sd
```

# Installing packages - remember use opkg
```shell
$ opkg update
$ opkg install curl
```

# Connect via usb
If IP address not automatically configured...
1. Determine interface:
```shell
$ sudo ifconfig
```
2. Then enable interface. e.g.
```shell
$ sudo ifconfig enx00c0ca90d48d 172.16.42.42 netmask 255.255.255.0 up
```

