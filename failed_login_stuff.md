# As root:
```shell
$ cat /var/log/auth.log | grep 'sshd.*Invalid'
```

# For successful logins:
```shell
$ cat /var/log/auth.log | grep 'sshd.*opened'
```
