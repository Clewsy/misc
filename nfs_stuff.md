# Installation
Ensure nfs-common package is installed
```shell
$ sudo apt update && sudo apt install nfs-common
```

# Manual access
Create local mount point
``shell
$ sudo mkdir /mnt/[local_path]
```
Mount
```shell
$ sudo mount [hostname]:/[remote_path] [local_path]
```

# Example
```shell
$ sudo mkdir /mnt/D4T4
$ sudo mount zapp:/export/D4T4
```

# Automatic access
Add item to fstab
```shell
$ sudo vim /etc/fstab
```
Add the nfs share as a new line item:
```shell
...
[hostname]:/[remote_path]	[local_path]	nfs	auto,rw,user,intr,bg	0	0
```
Notes:
* `auto` : Automatically detect the filesystem type. 
* `rw` : Mount will have read-write access.
* `user` : Allows the filesystem to be mounted by any user.
* `intr` : Allow signals to interrupt file operations on this mount point.
* `bg` : "Background" nfs mount - a timeout or failure causes mount to for a child that will continue to attempt the mount.


# Example
```shell
$ sudo vim /etc/fstab
```
Add the following:
```shell
...
zapp:/export/D4T4	/mnt/D4T4	nfs	auto,rw,user,intr,bg	0	0
```
