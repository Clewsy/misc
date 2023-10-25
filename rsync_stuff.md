# rsync stuff

## typical usage options
```shell
rsync -a -v -h --progress traget destination
# -a | --archive    ## Archive mode, equivalent to -rlptgoD (no -H, -A, -X).
# -v | --verbose
# -h | --human-readable
#      --progress
# -r | --recursive  ## Not needed if -a is specified.
#
# Note using --archive is equivalent to:
# -r | --recursive
# -l | --links (copy symlinks as symlinks)
# -p | --perms (preserve permissions)
# -t | --times (preserve modification times)
# -g | --group (preserve group)
# -o | --owner (preserve owner when run as superuser)
# -D | --devices preserve device files when run as superuser)
```

