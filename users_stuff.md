# Add a new user
```shell
$ sudo adduser b4t
```

# Add a user to sudo group
```shell
$ usermod -aG sudo b4t
```

# Check groups to which user is a member
```shell
$ groups b4t
```

# Remove a user
```shell
$ sudo deluser --remove-home b4t
```

# Enable root login for removing default user/s and adding new
```shell
$ sudo echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
$ sudo service sshd restart
```
