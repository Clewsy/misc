# Encrypt a file
```shell
$ gpg -c file.txt
```
Enter passphrase (x2)

Where: -c : Encrypt with a symmetric cipher using a passphrase.  Default cipher is AES128

Note, encrypted file (file.txt.gpg) is created but original file is retained.
```shell
$ rm file.txt
```


# Decrypt a file
Output encrypted file contents to stdout:
```shell
$ gpg -d file.txt.gpg
```

Create a new, decrypted file:
```shell
$ gpg -d -o file.txt file.txt.gpg
```


# Disable cacheing of keys by gpg-agent
```shell
$ vim ~/.gnupg/gpg-agent.conf
```
Add to file:
```shell
default-cache-ttl 0
max-cache-ttl 0
```
Enable:
```shell
$ gpgconf --reload gpg-agent
```

