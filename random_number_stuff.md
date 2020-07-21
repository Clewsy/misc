# Generate a random number:
```shell
$ echo $RANDOM
```

# Seed with epoch time:
```shell
$ RANDOM=$(date +%s)
```

# Generate within a range, e.g. between 0 and 128:
```shell
$ NUMB=$(( $RANDOM % 129 ))
```
