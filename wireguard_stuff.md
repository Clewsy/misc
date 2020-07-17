
# Key generation

Create private key.
```shell
$ uamsk 077
$ wg genkey > privatekey
```

Create public key.
```shell
$ wg pubkey < privatekey > publickey
```

# Server setup

Install wireguard.

Open ufw firewall port on server.
```shell
$ ufw allow 55505/udp
```

Enable routing on the server.
```shell
$ sudo echo "net.ipv4.ip_forward = 1
net.ipv6.conf.all.forwarding = 1" >> /etc/sysctl.d/wg.conf

$ sudo sysctl --system
```

Move and rename server config file.
```shell
$ sudo mv wg_clews_server_wg0.conf /etc/wireguard/wg0.conf
```

Start wg with the conf file and enable start at boot.
```shell
$ sudo systemctl start wg-quick@wg0
$ sudo systemctl enable wg-quick@wg0
```

# Client setup android

Install wireguard app (from fdroid).

Generate qr code from client conf file.
May need to install qrencode.
```shell
qrencode -t ansiutf8 < wg_clews_client.conf
```

# Client setup ubuntu/debian
Have the client conf file ready: **wg_clews_client_nibbler.conf**
```shell
$ sudo cp wg_clews_client_nibbler.conf /etc/wireguard/wg0.conf
$ sudo wg-quick up wg0
```
