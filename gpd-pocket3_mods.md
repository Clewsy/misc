# Usability fixes and improvements and workarounds for the GPD-Pocket3 with Pop_OS and Wayland.

## Enable wayland in Pop+OS
Need to edit the file at **/etc/gdm3/custom.conf**.
```shell
WaylandEnable=false
```
Now when at the login screen the cog will be available to select a Wayland session.

## Get screen rotation working (including touch and stylus inputs).
1. Implement kernel parameter (**mem_sleep_default=s2idle**) to correct default orientation at boot.
Note, pop_os uses kernelstub for implementing kernel parameter changes.  The following may not work for other distros (e.g. Ubuntu uses grub) but the parameter itself should be the same.
```shell
$ sudo kernelstub -a video=DSI-1:panel_orientation=right_side_up
```
Note: verify the presence of the kernel parameter under *options*.
```shell
$ cat /boot/efi/loader/entries/Pop_OS-current.conf
```
2. Configure a translation matrix to correct orientation based on accellerometer sensor.
Create this file **/etc/udev/hwdb.b/61-sensor-local.hwdb** with the following:
```shell
sensor:modalias:*
  ACCEL_MOUNT_MATRIX=0, -1, 0; -1, 0, 0; 0, 0, 1
```
Enable the above with the following command:
```shell
$ sudo systemd-hwdb update && \
sudo udevadm trigger -v -p DEVNAME=/dev/iio:device0  && \
sudo systemctl restart iio-sensor-proxy.service
```
3. Install the *Screen Rotate* gnome-shell extension:
```shell
$ git clone https://github.com/kosmospredanie/gnome-shell-extension-screen-autorotate.git
$ cd gnome-shell-extension-screen-autorotate
$ cp -r screen-autorotate@kosmospredanie.yandex.ru ~/.local/share/gnome-shell/extensions
```
Enable the extension (need to log outthen back in again to load new extension).
```shell
$ gnome-extensions enable screen-rotate@shyzus.github.io
```

## Enable wayland for firefox - fixes touchscreen scrolling.
Create file **/etc/environment.d/99-firefox-wayland.conf** with the following text:
```shell
#Enable wayland for firefox - fixes touchscreen scrolling.
MOZ_ENABLE_WAYLAND=1
```
Will require a reboot.

## Single-touch open in nautilus (touble-tap is buggy with touchscreen).
Preferences -> Action to Open Items -> Set to "Single Click"

## Get rid of "gjs" mystery app (visible from alt-tab menu).
This is due to using Wayland and the "Desktop Icons NG" extension.  Just disable the extension.
```shell
$ gnome-extensions disable ding@rastersoft.com
```

## Guake dropdown with F12 fix
This is a bug with Guake on wayland - https://github.com/Guake/guake/issues/492

Fix is to assign the command *guake -t* to F12 as a custom keyboard shortcut.

## Fix suspend by forcing S2 suspend (instead of S3).
Need to add the kernel parameter **mem_sleep_default=s2idle**.  To make this parameter survive a reboot, use the kernelstub command in Pop_OOS.
```shell
sudo kernelstub -a mem_sleep_default=s2isle
```
Note: verify the presence of the kernel parameter under *options*.
```shell
$ cat /boot/efi/loader/entries/Pop_OS-current.conf
```
