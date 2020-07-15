# as root:
```shell
$ cat /var/log/auth.log | grep 'sshd.*Invalid'
```

# for successful logins:
```shell
$ cat /var/log/auth.log | grep 'sshd.*opened'
```
