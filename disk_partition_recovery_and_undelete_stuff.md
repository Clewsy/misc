# Undelete from command line.

Use tool *testdisk*
```shell
$ sudo apt update && sudo apt install testdisk
```

# Fix ntfs disk

This worked when an external USB ntfs disk partition (/dev/sda1) stopped mounting in linux.

Use the *ntfsfix* util included withthe *ntfs-3g* package.

```shell
# sudo apt update && sudo apt install ntfs-36
$ sudo ntfs -b /dev/sda1

```

