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
