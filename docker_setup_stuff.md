# Install docker and set up

## 1 Install Docker

```shell
$ sudo apt-get update
$ sudo apt-get dist-upgrade
$ sudo apt-get install docker.io
```

consider rebooting

enable docker daemon
```shell
$ sudo systemctl enable docker.service
$ sudo systemctl start docker.service
```

## 2 Install docker-compose

download latest docker-compose binary to the /usr/local/bin directory
```shell
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

make it executable
```shell
$ sudo chmod +x /usr/local/bin/docker-composei
```

## 3 Set up docker group
```shell
$ sudo groupadd docker
$ sudo usermod -aG docker jc
```

## 4 Set up firewall
```shell
$ sudo ufw allow OpenSSH	#opens port 22
$ sudo ufw allow http		#opens port 80
$ sudo ufw allow https		#opens port 443
$ sudo ufw enable
$ sudo ufw status
```

## Addendum
good guide for nextcloud:
https://blog.ssdnodes.com/blog/installing-nextcloud-docker/
