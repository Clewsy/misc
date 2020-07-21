# Configuration file
```shell
$ sudo vim /etc/ssmtp/ssmtp.conf
```

# Setup
Uncomment `FromLineOverride=YES` by deleting the `#`
Add the following to the file:
```shell
AuthUser=<user>@gmail.com
AuthPass=Your-Gmail-Password
mailhub=smtp.gmail.com:587
UseSTARTTLS=YES
```

# Example mail send
```shell
$ echo "Game over..." | mail -s "Status" -r "BBB <clewsy@address.com>" clewsy@other_address.com
```

