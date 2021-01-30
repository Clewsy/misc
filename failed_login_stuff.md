# As root:
```shell
$ sudo cat /var/log/auth.log | grep 'sshd.*Invalid'
```

# For successful logins:
```shell
$ sudo cat /var/log/auth.log | grep 'sshd.*opened'
```
