
# Get screen rotation working.

Create this file **/etc/udev/hwdb.b/61-sensor-local.hwdb** with the following:

```shell
sensor:modalias:*
  ACCEL_MOUNT_MATRIX=0, 1, 0; -1, 0, 0; 0, 0, 1
```

Enable the above with the following command:

```shell
$ sudo systemd-hwdb update && \
sudo udevadm trigger -v -p DEVNAME=/dev/iio:device0  && \
sudo systemctl restart iio-sensor-proxy.service
```

Install the *Screen Rotate* Gnomei-shell extension:
```shell
$ git clone https://github.com/kosmospredanie/gnome-shell-extension-screen-autorotate.git
$ cd gnome-shell-extension-screen-autorotate
$ cp -r screen-autorotate@kosmospredanie.yandex.ru ~/.local/share/gnome-shell/extensions
```

Enable the extension (need to log outthen back in again to load new extension).
```shell
$ gnome-extensions enable screen-rotate@shyzus.github.io
```


# Enable wayland for firefox - fixes touchscreen scrolling.

Create file **/etc/environment.d/99-firefox-wayland.conf** with the following text:
```shell
#Enable wayland for firefox - fixes touchscreen scrolling.
MOZ_ENABLE_WAYLAND=1
```

Will require a reboot.

# Improve OSK usability

Install **Improved OSK** gnome extension.
```shell
$ git clone https://github.com/nick-shmyrev/improved-osk-gnome-ext.git ~/.local/share/gnome-shell/extensions/improvedosk@nick-shmyrev.dev
```

Enable the extension (need to log outthen back in again to load new extension).

```shell
$ gnome-extensions enable improvedosk@nick-shmyrev.dev
```

# Single-touch open in nautilus (touble-tap is buggy with touchscreen).

Preferences -> Action to Open Items -> Set to "Single Click"

# Get rid of "gjs" mystery app (visible from alt-tab menu).

This is due to using Wayland and the "Desktop Icons NG" extension.  Just disable the extension.

```shell
$ gnome-extensions disable ding@rastersoft.com
```

# Guake dropdown with F12 fix

This is a bug with Guake on wayland - https://github.com/Guake/guake/issues/492

Fix is to assign the command *guake -t* to F12 as a custom keyboard shortcut.


