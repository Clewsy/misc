## usb connection
if an ip is not automatically set up
1) determine interface name
```shell
ifconfig
```
2) assign static ip to interface
```shell
ifconfig <interface> 172.16.84.2 netmask 255.255.255.0 up
```

## access
ssh root@172.16.84.1
