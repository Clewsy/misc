# Set up wifi using cli
```shell
$  connmanctl 
connmanctl> 
connmanctl> scan wifi 
Scan completed for wifi

connmanctl> services 
$SSID    wifi_f8d111090ed6_6d617269636f6e5f64655f6d6965726461_managed_psk
...      ...

connmanctl> agent on
Agent registered

connmanctl> connect wifi_f8d111090ed6_6d617269636f6e5f64655f6d6965726461_managed_psk 
Agent RequestInput wifi_f8d111090ed6_6d617269636f6e5f64655f6d6965726461_managed_psk
Passphrase = [ Type=psk, Requirement=mandatory, Alternates=[ WPS ] ]
WPS = [ Type=wpspin, Requirement=alternate ]
Passphrase? $PASS
Connected wifi_f8d111090ed6_6d617269636f6e5f64655f6d6965726461_managed_psk

connmanctl> quit
```

# Set up wifi manually
```shell
$ cat << EOF > /var/lib/connman/<SSID>-psk.config
[service_wifi_<hash>_managed_psk]
Type = wifi
Name = <SSID>
Passphrase = <passphrase>
EOF
```
