##Reminder, uses dropbear for ssh.  Keys and authorized_keys at /etc/dropbear

##link to latest firmware for Linksys WRT32X
#https://openwrt.org/toh/linksys/linksys_wrt32x
opkg update && opkg install	luci-app-ddns \
				curl \
				luci-app-adblock \
				luci-ssl-openssl \
				wireguard \
				luci-app-wireguard \
				qrencode \
				luci-mod-rpc



#ddns client
#install software - luci-app-ddns - will automatically install dependencies
#install software - curl - ddns app will use curl if it is installed.
#guide for namecheap: http://electropit.com/index.php/2015/10/16/openwrt-ddns-setup-for-namecheap/
opkg install luci-app-ddns curl

#adblock
#install software - luci-app-adblock
#lan interface - USe custom DNS servers - set to 192.168.1.1
#wan inteface - advanced settings - Use custom DNS servers - set to 192.168.1.1 and 1.1.1.1
#!! Ensure luci-ssl-openssl package is installed (will automatically install libustream-openssl)
#confirm that openwrt->Services->Adblock page shows a result under "Overall Domains" (i.e. non-zero).
opkg install luci-app-adblock luci-ssl-openssl

#wireguard - openwrt setup
#install software wireguard, wireguard-tools, luci-app-wireguard and luci-proto-wireguard (and maybe kmod-wireguard?)
#also qrencode for displaying, you guessed it, qr codes through the webui.
opkg install wireguard luci-app-wireguard
#to create wireguard keys:
wg genkey > wg_privkey			##Create the private key
wg pubkey < wg_privkey > wg_pubkey	##Derive the public key from the private key
#create a new interface with "Wireguard" protocol
#General setup:
##Protocol=		"WireGuard VPN"
##Private Key=		<copy here, see above>
#Listen Port=		"50005"
#IP Addresses=		"fd00:6d61:7261::11/64"
#			"10.10.10.1/24"
#####
#Peers:
#Public Key=		<copy from device (e.g. android)>
#Allowed IPs=		"fd00:6d61:7261::/48
#			"10.10.10.2/24"
#Route Allowed IPs=	<yes (check)>
#Persistent Keep Alive=	"25"
#
#Firewall settings:
#Add to "lan" firewall zone.
#
#Network->Firewall->Traffic Rules
#Add new rule:
#Name=				"Allow-Wireguard-Inbound"
#Restrict to address family=	"IVP4 and IPV6"
#Protocol=			"UDP"
#Source Zone=			"wan"
#Source MAC address=		"any"
#Source address=		"any"
#Source port=			"any"
#Destination zone=		"Device (input)"
#Destination address=		"any"
#Destination port=		"50005"
#Action=			"accept"
#
#
##########
#wireguard - android setup
#Interface:
#Name=			"b4t-tunnel"
#Private key=		<generate>
#Public key=		<generated>
#Addresses=		"10.10.10.2/24, fd00:6d61:7261::/48"
#DNS servers=		"192.168.1.1"
#
#Peer:
#Public key=		<copy from openwrt>
#Allowed IPs=		"0.0.0.0, ::/0
#Endpoint=		"b4t.site:50005"
#Persistent keepalive=	"25"
#
#
######## For hass.io precense detection integration with luci:
opkg install luci-mod-rpc
