# Connect to phone/termux over ssh

Consider setting password on phone/termux.
```shell
$ passwd
```

Initiate sshd on phone/termux.
```shell
$ sshd
```

Over lan connect to phone/termux using default port 8022.
```shell
$ ssh phone_hostname_or_ip -p 8022
```

