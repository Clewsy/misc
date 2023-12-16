# Install
```shell
$ sudo apt-get install motion
```

# Configure camera
```shell
$ vim /etc/motion/motion.conf
```
Useful options to customise:
```shell
daemon on                   ##enables the daemon
framerate 100               ##default is 2 (lowest)
stream_port 8890            ##or whatever port
stream_quality 100
stream_localhost OFF        ##setting OFF allows external viewing
webcontrol_localhost OFF
quality 100
width 640
height 480
post_capture 5
 
stream_auth_method 2    ##enable hashed authentication
stream_authentication username:password
 
ffmpeg_output_movies off    ##disable recording video to files
output_pictures off         ##disable recording image (jpg) files
```

# Configure service
```shell
$ vim /etc/default/motion
```
Enable daemonisation at boot:
```shell
start_motion_daemon=yes ##enable daemon autostart
```

# Restart service
```shell
$ sudo service motion restart
```

# Start motion
```shell
$ sudo reboot
```
Or
```shell
$ motion
```

