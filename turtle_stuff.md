# lan turtle

## USB connection
If an ip is not automatically set up
1) Determine interface name
```shell
$ ifconfig
```
2) Assign static ip to interface
```shell
$ ifconfig <interface> 172.16.84.2 netmask 255.255.255.0 up
```

## Access
```shell
$ ssh root@172.16.84.1
```
Factory password: sh3llz

Note, by default, ssh client access is only possible via eth0 (USB adapter).  To enable ssh client access via eth1 (ethernet), modify the firewall config:

### /etc/config/firewall

Change:
```shell
config zone
        option name             wan
        list   network          'wan'
        list   network          'wan6'
        option input            REJECT
```

To:
```shell
config zone
        option name             wan
        list   network          'wan'
        list   network          'wan6'
        option input            ACCEPT
```

## Firmware

### HAK 5
https://downloads.hak5.org/turtle

### OpenWRT
https://openwrt.org/toh/hwdata/hak5/hak5_lan_turtle

