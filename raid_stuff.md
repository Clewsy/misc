# Partition Stuff

## Create an ext4 partition.

Determine which device:
```shell
$ sudo fdisk -l
```

Run fdisk:
```shell
$ sudo fdisk /dev/sdb
```
1. Press 'g' to create a new empty partition table (gpt for modern UEFI booting).
2. Press 'n' to create a new partition.
3. Set partition number, first sector, last sector.
4. Verify by pressing 'p'.
5. Commit changes and quit with 'w'.

Activate the partition by formatting and mounting to the system's directory tree.  This is required so that the disks will be identifiable under /dev/disk/by-###:
```shell
$ sudo mkfs.ext4 -F /dev/sdb1
```

## Configure a raid mirror (RAID1).

Install prerequisites.
```shell
$ sudo apt install mdadm #May not be needed - preinstalled on ubuntu server.
```

Partition disks.
```shell
$ sudo fdisk /dev/sdX #Where X is the drive to configure.
```
1. Press ‘n‘ for creating new partition.
2. Then choose ‘P‘ for Primary partition.
3. Next select the partition number as 1.
4. Give the default full size by just pressing two times Enter key.
5. Next press ‘p‘ to print the defined partition.
6. Press ‘l‘ to list all available types.
7. Type ‘t‘ to choose the partitions.
8. Choose ‘fd‘ for Linux raid auto and press Enter to apply.
9. Then again use ‘p‘ to print the changes what we have made.
10. Use ‘w‘ to write the changes.

Repeat for second disk.

Verify the changes on disks (e.g. /dev/sdb and /dev/sdc)
```shell
$ sudo mdadm -E /dev/sd[b-c]1
mdadm: No md superblock detected on /dev/sdb1
mdadm: No md superblock detected on /dev/sdc1
```

Create RAID1 devices.
```shell
$ sudo mdadm --create /dev/md0 --level=mirror --raid-devices=2 /dev/sd[b-c]1
mdadm: Note: this array has metadata at the start and
    may not be suitable as a boot device.  If you plan to
    store '/boot' on this device please ensure that
    your boot-loader understands md/v1.x metadata, or use
    --metadata=0.90
Continue creating array? y
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.
```
Wait until raid creation is complete:
```shell
$ watch cat /proc/mdstat
Every 2.0s: cat /proc/mdstat

Personalities : [linear] [multipath] [raid0] [raid1] [raid6] [raid5] [raid4] [raid10] 
md0 : active raid1 sde1[1] sdd1[0]
      234297920 blocks super 1.2 [2/2] [UU]
      [>....................]  resync =  3.1% (7337856/234297920) finish=75.5min speed=50082K/sec
      bitmap: 2/2 pages [8KB], 65536KB chunk

unused devices: <none>
```
Check raid devices type and raid array:
```shell
$ sudo mdadm -E /dev/sd[b-c]1
...
	Raid Level   : raid1
	Raid Devices : 2
...
$ sudo mdadm --detail /dev/md0
...
	State           : clean
	Active Devices  : 2
	Working Devices : 2
	Failed Devices  : 0
	Spare Devices   : 0
...
```
Create file system on raid device.
```shell
$ sudo mkfs.ext4 /dev/md0
mke2fs 1.45.5 (07-Jan-2020)
Discarding device blocks: done                            
Creating filesystem with 58574480 4k blocks and 14647296 inodes
Filesystem UUID: 0650992b-c39e-4a30-8cc8-90ac94503b59
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
	4096000, 7962624, 11239424, 20480000, 23887872

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (262144 blocks): done
Writing superblocks and filesystem accounting information: done
```

Can now asign a label and mount like a standalone disk.
```shell
$ sudo e2label /dev/md0 raid_label
$ sudo mount /dev/md0 /mnt/mounted_raid
```
