# Bulk file upload

## Use webdav to browse files from nautilus.
Address to use in nautilus:
davs://example.com/nextcloud/remote.php/dav/files/USERNAME/

## Copy files
Use rsync to bulk upload to nextcloud instance:
```shell
$ rsync -v -r --progress [directory] [user]@[server]:~/cloud/[target]
```
This assumes symbolic link "cloud" directs to cloud files e.g. /var/www/html/nextcloud/data/user/files/

## Set user/group and permission
Permissions must be set accordingly on the remote machine.
For example, make user a member of group www-data and give group www-data write access to the nextcloud dir.
```shell
$ sudo usermod -aG www-data user
$ sudo chmod -R g+w /var/www/html/nextcloud
```

## Set permissions for copied files
```shell
$ sudo chown -R www-data:www-data /var/www/html/nextcloud
```

## Run nextcloud script to scan for new files and update database.
```shell
$ cd /var/www/html/nextcloud
$ sudo -u www-data php occ files:scan --all
```

## Above scan but for use with a docker container
```shell
$ docker exec -u www-data nextcloud-app php occ files:scan --all -v
```

