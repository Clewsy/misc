# Default web interface ip
172.16.42.1:1471
(Just plug in via usb and this ip should work after it boots)

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
$ cd /sd
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

# Firmware Installation/Recovery

A link to the hak5 guidance and image downloads:
https://docs.hak5.org/wifi-pineapple-6th-gen-nano-tetra/faq-troubleshooting/firmware-recovery

This firmware install feature can also be used to install openWRT!

## Instructions:
- Unplug the WiFi Pineapple completely from all power sources.
- Begin holding the RESET button on the device.
- With the RESET button held, power on the device.
- Continue holding the RESET button for 10 seconds, then release.  The blue LED will remain solid
- Connect the host PC to the WiFi Pineapple via the USB Ethernet Port (the male USB A plug).
- From the host PC, configure a static IP address on the WiFi Pineapple facing Ethernet interface to 192.168.1.2 with netmask 255.255.255.0
- For example, in Linux run:
 ```shell
$ sudo ifconfig eth1 192.168.1.2 netmask 255.255.255.0 up #(where eth1 is the interface name of the WiFi Pineapple).
```
- From the host PC, browse to http://192.168.1.1
- Click Choose File and select the factory firmware image downloaded above.
- Click Update Firmware.
- This process will take several minutes. Do not interrupt the power supply while the firmware is updating. Once complete, the WiFi Pineapple will restart.
- Reset the the WiFi Pineapple facing USB Ethernet interface back to DHCP or 172.16.42.42 with netmask 255.255.255.0

# OpenWRT on the pineapple nano

Link to the firmware downolad page:
https://openwrt.org/toh/hwdata/hak5/hak5_wifi_pineapple_nano

## Create a WiFi AP from a LAN connection.
1. Install the driver for the USB-Ethernet adapter (e.g. kmod-usb-net-asix).  Install software from "System"->"Software" (don't forget to "Update lists...).
2. Add the network device to the existing interface "lan" (br-lan). "Network"->"Interfaces".  "Devices" tab. "br-lan" => "Configure".  Add "eth1" to "Bridge ports".
3. Configure interface "br-lan" to be a DHCP client and obtain its IP from the LAN.  "Network"->"Interfaces". "lan" interface -> "Edit".  Set "Protocol" to "DHCP client".
4. Create a wireless access point and be sure to add it to the "lan" inteface to effectively bridge it to the ethernet connections.
5. Some restarting may be needed along the way.
