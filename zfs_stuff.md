# zfs

## install zfsutils-linux

```shell
$ sudo apt install zfsutils-linux
```

## create a zfs pool

```shell
## will mount pool_name at /pool_name
$ sudo zpool create pool_name /dev/sdX /dev/sdY

## will mount pool_name at /data/pool_name
$ sudo zpool create -m /data/pool_name pool_name /dev/sdX /dev/sdY

```
## create a zfs dataset

``` shell
$ zfs create pool_name/dataset_name
```

## list datasets

```shell
$ zfs list
```

## show dataset mountpoint

```shell
$ zfs get mountpoint dataset_name
```

## change dataset or pool mountpoint

```shell
## entire pool:
$ zfs set mountpoint=/path/to/mountpoint pool_name
## dataset:
$ zfs set mountpoint=/path/to/mountpoint pool_name/dataset_name
```

## export a pool

```shell
$ zpool export pool_name

## If busy, can be forced:
$ zpool export -f pool_name
```

## import a zpool

```shell
## identify available pools:
$ zpool import

## import a specific pool:
$ zpool import pool_name

## if devices change
$ zpool import -a -d /dev/disk/by-id
```

## delete a dataset

```shell
$ zfs destroy dataset_name
```

## delete a pool
```shell
$ zpool destroy pool_name
```

