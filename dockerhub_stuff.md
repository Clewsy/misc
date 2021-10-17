# Push container image to dockerhub.

First build the image to update any changes made.
```shell
$ cd ncbu
$ docker build -t clewsy/ncbu .
```

Login to dockerhub account.

```shell
$ docker login
```
Enter credentials.  Note, password must be an access token, not the general login password.

Apply image tag if required.
```shell
$ docker tag 1.1 clewsy/ncbu
```

Push the image to dockerhub.
```shell
$ docker push clewsy/ncbu
```

Job done.
HOWEVER - if changes do not affect layers (e.g. README update) you will need to manually update for some reason.
