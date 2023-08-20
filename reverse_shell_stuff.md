# reverse shell

## usage

```shell
$ ssh -N -R 44444:localhost:22 -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null user@servername_or_ip
```
Where:
                                 -N : Do not execute a remote command (just forwarding ports).
                                 -R : Specifies that the given connection on the remote server will be forwarded to the local side.
                              44444 : port - used from the server to connect to the reverse ssh host.
                          localhost : define the reverse ssh host.
                                 22 : ssh port used to connect to the reverse ssh host
              user@servername_or_ip : the remote server that will have access to the reverse ssh host.
        -o StrictHostKeyChecking=no : Disable checking of the server's public key fingerprint against known_hosts list.
    -o UserKnownHostsFile=/dev/null : Disable saving the host in the known_hosts list.

## example

Establish reverse ssh connection from the reverse ssh host.
```shell
$ ssh -N -R 44444:localhost:22 -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null user@servername_or_ip
```

Connect to the reverse ssh host from the server.
```shell
$ ssh -p 44444 user@localhost
```

