# zapp

How to configure openmediavault via gui.

## Initial login

Webui default credentials are:
* Username: admin
* Password: openmediavault

# System

## General Settings

### Web Administration

General settings
* Auto logout: 1 day

### Web Administrator Password

Set new password

## Certificates

### SSH

Add -> Import: user@host
* Private key -> copy from id_rsa
* Public key -> Copy from id_rsa.pub
* Comment: user@host

# Storage

## Disks

No changes, but check they're all there:

| Device   | Model            | Capacity  |
|----------|------------------|-----------|
| /dev/sda | Corsair CMFSSD-6 | 59.63 GiB |
| /dev/sde | KINGSTON SA40053 | 11.79 GiB |
| /dev/sdd | KINGSTON SA40053 | 11.79 GiB |
| /dev/sdc | ST4000DM004-2CV1 | 3.64 TiB  |
| /dev/sdb | WDC WD15EADS-11P | 1.36 TiB  |

## S.M.A.R.T.

### Devices

Turn on **Monitor** for:
* /dev/sdc
* /dev/sdd
* /dev/sde

## RAID Management

No changes, but check mirror is detected:
* host:cl0ud -> /dev/md127 -> clean -> Mirror -> 111.73 GiB ->
	* /dev/sdd
	* /dev/sde

## File Systems

Mount all except swap (/dev/sda5)

| Device     | Label         | Filesystem Type | Total     |
|------------|---------------|-----------------|-----------|
| /dev/sda1  | none (system) | ext4            | 46.66GiB  |
| /dev/sda5  | none (swap)   | swap            | n/a       |
| /dev/md127 | cl0ud         | ext4            | 109.47GiB |
| /dev/sdc1  | f1leb0t       | ext4            | 3.58TiB   |
| /dev/sdb1  | m0n0l1th      | ext4            | 1.34TiB   |

# Access Rights Management

## User

### Users

No changes, but check groups for user:
* user
* sudo
* ssh
* docker

## Shared Folders

Add each of the following:

| Name            | Device   | Relative Path    |
|-----------------|----------|------------------|
| cl0ud           | cl0ud    | /                |
| data            | f1leb0t  | data/            |
| docker_zoidberg | cl0ud    | docker_zoidberg/ |
| file_cache      | cl0ud    | file_cace/       |
| m0n0l1th        | m0n0l1th | /                |
| movies          | f1leb0t  | movies/          |
| mp3s            | f1leb0t  | mp3s/            |
| music_videos    | f1leb0t  | music_videos/    |
| tv              | f1leb0t  | tv/              |

# Services

## NFS

### Settings

Enable

### Shares

Add each of the following:

| Shared folder | Client         | Options                                  |
|---------------|----------------|------------------------------------------|
| cl0ud         | 192.168.1.0/24 | rw,subtree_check,insecure,no_root_squash |
| data          | 192.168.1.0/24 | rw,subtree_check,insecure,no_root_squash |
| m0n0l1th      | 192.168.1.0/24 | rw,subtree_check,insecure,no_root_squash |
| movies        | 192.168.1.0/24 | rw,subtree_check,insecure,no_root_squash |
| mp3s          | 192.168.1.0/24 | rw,subtree_check,insecure,no_root_squash |
| music_videos  | 192.168.1.0/24 | rw,subtree_check,insecure,no_root_squash |
| tv            | 192.168.1.0/24 | rw,subtree_check,insecure,no_root_squash |

## Rsync

### Jobs

Add and enable each of the following:

| Type   | Source                       | Destination                              | Comment                                  |
|--------|------------------------------|------------------------------------------|------------------------------------------|
| Remote | clewsy@zoidberg:/home/docker | docker_zoidberg                          | daily_0100hrs docker_zoidberg zoid->zapp |
| Remote | docker_zoidberg              | user@user.site:~/backups/docker_zoidberg | daily_0200hrs docker_zoidberg zapp->user |
| Remote | user@seymour:~/file_cache    | cl0ud                                    | daily_0300hrs file_cache seymour->zapp   |
| Remote | file_cache                   | user@user.site:~/backups/file_cache      | daily_0400hrs file_cache zapp->user      |

Specific settings for these shares:

1. daily_0100hrs docker_zoidberg zoid->zapp
	* Enable: check
	* Type: Remote
	* Mode: Pull
	* Source server: clewsy@zoidberg:/home/docker
	* Destination shared folder: docker_zoidberg
	* Authentication: Public key
	* SSH port: 22
	* SSH certificate: user@zapp
	* Minute: 0
	* Hour: 1
	* Turn on:
		* Archive
		* Recursive
		* Preserve permissions
		* Preserve modification times
		* Preserve group
		* Preserve owner
		* Preserve ACLs
		* Delete
	* Extra options: --human-readable
	* Comment: daily_0100hrs docker_zoidberg zoid->zapp
2. daily_0200hrs docker_zoidberg zapp->user
	* Enable: check
	* Type: Remote
	* Mode: Push
	* Source shared folder: docker_zoidberg
	* Destination server: user@user.site:~/backups/docker_zoidberg
	* Authentication: Public key
	* SSH port: 22
	* SSH certificate: user@zapp
	* Minute: 0
	* Hour: 2
	* Turn on:
		* Archive
		* Recursive
		* Preserve permissions
		* Preserve modification times
		* Preserve group
		* Preserve owner
		* Preserve ACLs
		* Delete
	* Extra options: --human-readable
	* Comment: daily_0200hrs docker_zoidberg zapp->user
3. daily_0300hrs file_cache seymour->zapp
	* Enable: check
	* Type: Remote
	* Mode: Pull
	* Source server: user@seymour:~/file_cache
	* Destination shared folder: cl0ud
	* Authentication: Public key
	* SSH port: 22
	* SSH certificate: user@zapp
	* Minute: 0
	* Hour: 3
	* Turn on:
		* Archive
		* Recursive
		* Preserve permissions
		* Preserve modification times
		* Preserve group
		* Preserve owner
		* Preserve ACLs
	* Extra options: --human-readable
	* Comment: daily_0300hrs file_cache seymour->zapp
4. daily_0400hrs file_cache zapp->user
	* Enable: check
	* Type: Remote
	* Mode: Push
	* Source shared folder: file_cache
	* Destination server: user@user.site:~/backups/file_cache
	* Authentication: Public key
	* SSH port: 22
	* SSH certificate: user@zapp
	* Minute: 0
	* Hour: 4
	* Turn on:
		* Archive
		* Recursive
		* Preserve permissions
		* Preserve modification times
		* Preserve group
		* Preserve owner
		* Preserve ACLs
	* Extra options: --human-readable
	* Comment: daily_0400hrs file_cache zapp->user

Remember to add keys to known hosts and test the rsync jobs.

