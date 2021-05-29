# Raspbian

## To enable headless ssh and wifi connection
Guide: https://www.raspberrypi.org/documentation/configuration/wireless/headless.md

## Enable ssh by creating a file calles "ssh" in the boot directory
```shell
$ touch /media/jc/boot/ssh
```

## Enable wifi connectivity by creating `wpa_supplicant.conf` file in the boot directory
```shell
$ vim /media/jc/boot/wpa_supplicant.conf
```
Enter into `wpa_supplicant.conf` the following:

```shell
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=AU

network={
    ssid="«your_SSID»"
    psk="«your_PSK»"
    key_mgmt=WPA-PSK
}
```

To avoid storing password in plain text, get the hashed password by using wpa_passphrase:
```shell
$ wpa_passphrase <your_SSID>
```
Then enter the corresponding passphrase.

Remember to store hashed passphrase without quotes.  I.e.:
```shell
	psk=bwbfwekjbhfkjwhbqwh83232dwc78...etc
```

Also remeber to change the default login (pi) and password (raspberry).


# Ubuntu

## Default login
Username: ubuntu
Password: ubuntu

## Configure sd card for wifi
In file */system-boot/network-config*

```yaml
wifis
  wlan0:
  dhcp4: true
  optional: true
  access-points:
    "B4T-Cave":
      password: "password"
```
Or hash password:
```yaml
    wifis:
        wlan0:
            access-points:
                "B4T-Cave":
                    password: 481dc47d86e25131512312351abc0d62fb3aef639etc
            dhcp4: true
            optional: true
```

**Note**: network name must be enclosed in quotation marks.

