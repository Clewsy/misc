# iptables stuff

### List current rules
```shell
$ iptables -L -v		#-L to list current rules, -v for verbose
```
Chain types:
- `INPUT`	This chain is used to control the behavior for incoming connections. 
- `FORWARD`	This chain is used for incoming connections that aren’t actually being delivered locally. Think of a router...
- `OUTPUT`	This chain is used for outgoing connections.

### Set default policies
Setting "policy" for the chains sets the default behaviour.  The following example sets defaults to accept connections.
```shell
$ iptables --policy INPUT ACCEPT
$ iptables --policy OUTPUT ACCEPT
$ iptables --policy FORWARD ACCEPT
```

Alternatively, following commands sets default to drop all connections
```shell
$ iptables --policy INPUT DROP
$ iptables --policy OUTPUT DROP
$ iptables --policy FORWARD DROP
```

Available actions for dealing with connections:
- Accept – Allow the connection.
- Drop – Drop the connection, act like it never happened.
- Reject – Don’t allow the connection, but send back an error.

This example shows how to block all connections from the IP address 10.10.10.10.
```shell
$ iptables -A INPUT -s 10.10.10.10 -j DROP
```
- -A to append chain (INPUT) with this rule
- -s to specify source ip (10.10.10.10)
- -j for jump to specify how to handle the connection (DROP)

This example shows how to block all of the IP addresses in the 10.10.10.0/24 network range.
You can use a netmask or standard slash notation to specify the range of IP addresses.
```shell
$ iptables -A INPUT -s 10.10.10.0/24 -j DROP
```
Or
```shell
$ iptables -A INPUT -s 10.10.10.0/255.255.255.0 -j DROP
```

This example shows how to block SSH connections from 10.10.10.10.
```shell
$ iptables -A INPUT -p tcp --dport ssh -s 10.10.10.10 -j DROP
```
- -p to specify protocol (e.g. tcp, udp)
- --dport to specify intended destination port # or protocol.

Or
```shell
$ iptables -A INPUT -p tcp --dport 22 -s 10.10.10.10 -j DROP
```

This example shows how to block SSH connections from any IP address.
```shell
$ iptables -A INPUT -p tcp --dport ssh -j DROP
```

In this example, SSH connections FROM 10.10.10.10 are permitted, but SSH connections TO 10.10.10.10 are not.  However, the system is permitted to send back information over SSH as long as the session has already been established, which makes SSH communication possible between these two hosts.
```shell
$ iptables -A INPUT -p tcp --dport ssh -s 10.10.10.10 -m state --state NEW,ESTABLISHED -j ACCEPT
$ iptables -A OUTPUT -p tcp --sport 22 -d 10.10.10.10 -m state --state ESTABLISHED -j ACCEPT
```
- -m to check for a match - in this case of state
- --sport to specify source port
- -d to define destination ip

This exmaple allows incoming and forwarding connections using tunnnel interface (e.g. when using a vpn).
```shell
$ iptables -A INPUT -i tun+ -j ACCEPT
$ iptables -A FORWARD -i tun+ -j ACCEPT
```

### Save changes to iptable
```shell
$ sudo /sbin/iptables-save
```

### Clear all the currently configured rules (flush)
```shell
$ iptables -F
 ```

# NAT network address translation
```shell
$ iptables -t nat <other stuff> #option to change the NAT table
```

The following example will make all packets sent out appear to have come from eth0, even if tun0 is active (openvpn)
```shell
$ iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```
- -t nat to specify changes to the NAT table.
- -A to append rule to the selected chain (POSTROUTING).
- POSTROUTING chain selected to alter the packet just before it is sent out.
- -o to set outgoing interface (eth0).
- -j for jump to set the action to apply to the packet (MASQUERADE).
- MASQUERADE  needed due to dynamic external IP address, so no source address is needed.  Also this way if the link goes down, connections are forgotten to avoid glitches when re-connecting from a different ip.
- POSTROUTING chain used to alter packet just before it is sent out. E.g. to change the source address.
- PREROUTING chain used to alter packet just as it comes in.

# Handy guides:
https://www.howtogeek.com/177621/the-beginners-guide-to-iptables-the-linux-firewall/

https://www.netfilter.org/documentation/HOWTO/NAT-HOWTO-6.html


