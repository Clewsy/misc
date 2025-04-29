# flatpak tips

## check flatpak disk usage
```shell
$ du -h /var/lib/flatpak    #the final line item is the total for the directory
$ ncdu /var/lib/flatpak     #alternative to see the breakdown.
```

## uninstall a flatpak
```shell
$ flatpak uninstall [tab-to-list-installed]
```

## clean up - uninstall un-used flatpaks
```shell
$ flatpak uninstall --unused
```
