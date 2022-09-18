# Find a MAC address on a network.

```shell
$ sudo arp -a # List all systems with hostname, IP and MAC.
$ sudo arp -a | grep be:b2 # Isolate entry by a known partial MAC address.
```
Note, if not found above, may have to first ping the IP address.  Alternatively, try arp-scan for the sub-net.

```shell
$ arp-scan 192.168.1.0/24
$ arp-scan | grep be:b2
```

# Force DHCP server to renew the IP address.
First, release.
```shell
$ sudo dhclient -v -r eth0
$ # -v : Verbose
$ # -r : Release
```
Second, request new.
```shell
$ sudo dhclient -v eth0
```

# Determine what ports are listening or have established connections.
```shell
$ lsof -i -P -n
```

# Change device MAC
To determine device name and current MAC:
```shell
$ ip link 
```
To change MAC (example for device eth0):
```shell
$ sudo ip link set dev eth0 down
$ sudo ip link set dev eth0 address b8:27:eb:75:36:0c
$ sudo ip link set dev eth0 up
```

# Set static IP
```shell
$ sudo ip addr add 192.168.1.132/24 dev eth0
```

