# Raspbian

## To enable headless ssh and wifi connection
Guide: https://www.raspberrypi.com/documentation/computers/configuration.html#setting-up-a-headless-raspberry-pi

## Enable ssh by creating a file calles "ssh" in the boot directory
```shell
$ touch /media/jc/boot/firmware/ssh
```

## Enable wifi connectivity by creating `wpa_supplicant.conf` file in the bootfs directory
```shell
$ vim /media/jc/bootfs/wpa_supplicant.conf
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

## Create a user
Raspberry Pi os now requires creation of a user for headless setups.
Add the username and encrypted password to file "userconf.txt" in the "bootfs" directory.
```shell
$ vim /media/jc/bootfs/userconf.txt
```

Add a user into the file with the following format:
```shell
username:<encrypted_password>
```

To generate the encrypted password use the command below and follow the prompts.
```shell
$ openssl passwd -6
```



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

