# Reminder, uses dropbear for ssh.  Keys and authorized_keys at /etc/dropbear

# Install packages:
```shell
$ opkg update && opkg install    luci-app-ddns \
                luci-app-adblock \
                luci-ssl-openssl \
                luci-app-wireguard \
                qrencode \
                luci-mod-rpc \
                luci-ssl
```


# ddns client
- install software - luci-app-ddns - will automatically install dependencies
- install software - curl - ddns app will use curl if it is installed.
- guide for namecheap: http://electropit.com/index.php/2015/10/16/openwrt-ddns-setup-for-namecheap/
```shell
$ opkg install luci-app-ddns curl
```

# adblock
- install software - luci-app-adblock
- lan interface - Use custom DNS servers - set to 192.168.1.1
- wan inteface - advanced settings - Use custom DNS servers - set to 192.168.1.1 and 1.1.1.1
- !! Ensure luci-ssl-openssl package is installed (will automatically install libustream-openssl)
- confirm that openwrt->Services->Adblock page shows a result under "Blocked Domains" (i.e. non-zero).  Try clicking "Reload".
```shell
$ opkg install luci-app-adblock luci-ssl-openssl
```

# wireguard - openwrt setup
- install software wireguard-tools and luci-proto-wireguard.  Just luci-proto-wireguard is sufficient and will grab required dependencies.
- also qrencode for displaying, you guessed it, qr codes through the webui.
```shell
$ opkg install luci-proto-wireguard qrencode
```

## create wireguard keys:
```shell
wg genkey > wg_privkey                ##Create the private key
wg pubkey < wg_privkey > wg_pubkey    ##Derive the public key from the private key
```

## Create a new interface with "Wireguard" protocol
General setup:
- Protocol=     "WireGuard VPN"
- Private Key=  <copy here, see above>
- Listen Port=  "50005"
- IP Addresses= "fd00:6d61:7261::11/64"
- IP Addressed= "10.10.10.1/24"
- Firewall Settings-> add to "lan" firewall zone.

Peers:
- Public Key=               <copy from device (e.g. android)>
- Allowed IPs=              "fd00:6d61:7261::/48
- Allowed IPs=              "10.10.10.2/24"
- Route Allowed IPs=        <yes (check)>
- Persistent Keep Alive=    "25"

## Firewall settings:
Network->Firewall->Traffic Rules->Add new rule:
- Name=                         "Allow-Wireguard-Inbound"
- Protocol=                     "UDP"
- Source Zone=                  "wan"
- Source address=               "any"
- Source port=                  "any"
- Destination zone=             "Device (input)"
- Destination address=          "any"
- Destination port=             "50005"
- Action=                       "accept"


## wireguard - android setup:
Interface:
- Name=         "b4t-tunnel"
- Private key=  <generate>
- Public key=   <generated>
- Addresses=    "10.10.10.2/24, fd00:6d61:7261::/48"
- DNS servers=  "192.168.1.1"

Peer:
- Public key=           <copy from openwrt>
- Allowed IPs=          "0.0.0.0, ::/0
- Endpoint=             "b4t.site:50005"
- Persistent keepalive= "25"


# hass.io presense detection integration with luci:
```shell
$ opkg install luci-mod-rpc
```

# https access to luci interface:
Installing luci-openssl will allow access to the luci interface with https (i.e. port 443).
```shell
$ opkg install luci-ssl
```

