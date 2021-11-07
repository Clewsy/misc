# Using dockerhub

## Push container image to dockerhub.

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

# Using gitlab container registry

Authenticate to the container registry.

With MFA/2FA - must create an access token.

In gitlab webui:
User_profile_icon_dropdown -> "Edit profile" -> "Access Tokens"
Select "api" as the token scope.

Now the container can be built and pushed (from with the project dir).

```shell
$ cd ~/projects/ncbu #Or wherever the project is located.
$ docker login registry.gitlab.com #Authenticate with the token created - see above.
$ docker build -t registry.gitlab.com/clewsy/ncbu .
$ docker push registry.gitlab.com/clewsy/ncbu
```

The container image can now be pulled/run with docker commands.

```shell
$ docker pull registry.gitlab.com/clewsy/ncbu
$ docker run registry.gitlab.com/clewsy/ncbu
```

It can also be pulled/run using docker-compose and a docker-compose.yml file.
```yml
######################################### Nextcloud backup container (for periodically copying data and database)
  nextcloud-bu:
    image: registry.gitlab.com/clewsy/ncbu
    container_name: nextcloud-bu
    network_mode: none
    depends_on:
      - nextcloud
      - nextcloud-db
    environment:
      - NEXTCLOUD_EXEC_USER=www-data                      # Name of the user that can execute the occ command in the nextcloud container (www-data by default).
      - NEXTCLOUD_CONTAINER=nextcloud                     # Name of the nextcloud container.
      - NEXTCLOUD_DATABASE_CONTAINER=nextcloud-db         # Name of the nextcloud database container.
      - NEXTCLOUD_BACKUP_CRON=0 0 * * *                   # Run at midnight.
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock         # Allows container to access another container.
      - /etc/localtime:/etc/localtime:ro                  # Use to sync time so that the crond runs as expected.
      - nextcloud-app:/mnt/nextcloud_app                  # Must match the docker-managed nextcloud app volume (/var/www/html).
      - nextcloud-db:/mnt/nextcloud_db                    # Must match the docker-managed nextcloud database volume (/var/lib/mysql).
      - ./nextcloud-bu:/backup                            # Convenient location for the backup.
    restart: unless-stopped

```




