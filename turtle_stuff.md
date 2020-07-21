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
$ ssh root@172.16.84.1

