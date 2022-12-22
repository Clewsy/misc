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
1. Need to add the kernel parameter **mem_sleep_default=s2idle**.  To make this parameter survive a reboot, use the kernelstub command in Pop_OOS.
```shell
sudo kernelstub -a mem_sleep_default=s2idle
```
Note: verify the presence of the kernel parameter under *options*.
```shell
$ cat /boot/efi/loader/entries/Pop_OS-current.conf
```
Note this means "standby" is really just idling and using much more power than true standby (to ram).  Therefore, reccomend using hibernation which needs some work to enable in Pop_OS:
2. Follow the [instructions here][https://support.system76.com/articles/enable-hibernation/] to enable Hibernation under Pop_OS.
[Enable Hibernation under op_OS][https://support.system76.com/articles/enable-hibernation/]
Test hibernation from the command line:
```shell
$ sudo systemctl hibernate
```
3. Install and enable the hibernation gnome extension.
```shell
# Looks like cloning from git only works for the latest version of gnome.
git clone https://github.com/arelange/gnome-shell-extension-hibernate-status.git ~/.local/share/gnome-shell/extensions/hibernate-status@dromi
```
```shell
$ # Note link below is for gnome 42 since the github repo only works for latest gnome.
$ wget https://extensions.gnome.org/extension-data/hibernate-statusdromi.v33.shell-extension.zip -O /tmp/hibernate-statusdromi.v33.shell-extension.zip
$ mkdir ~/.local/share/gnome-shell/extensions/hibernate-status@dromi
$ unzip /tmp/hibernate-statusdromi.v33.shell-extension.zip -d ~/.local/share/gnome-shell/extensions/hibernate-status@dromi
```
Enable the extension (need to log out then back in again to load new extension).
```shell
$ gnome-extensions enable hibernate-status@dromi
```
4. Pop_OS (and Ubuntu I think) require the following file:
```shell
$ sudo vim /etc/polkit-1/localauthority/10-vendor.d/com.ubuntu.pkla
```
Into it, copy the following:
```shell
[Enable hibernate in upower]
Identity=unix-user:*
Action=org.freedesktop.upower.hibernate
ResultActive=yes

[Enable hibernate in logind]
Identity=unix-user:*
Action=org.freedesktop.login1.hibernate;org.freedesktop.login1.handle-hibernate-key;org.freedesktop.login1;org.freedesktop.login1.hibernate-multiple-sessions;org.freedesktop.login1.hibernate-ignore-inhibit
ResultActive=yes
```
After a reboot, hibernate should be an option in the gui.

## Enable touch scroll for vscode under Wayland.
Need to run code withthe option **--touch-events**.  This only works if the option succeeds the file/directory you want to open in vscode.  Therefore a simple alias vsc="code --touch-events" will not work.  Well, it will implement touch scrolling, but will not open the desired file/directory.  Instead, add a function to the .bashrc file.
```shell
function vsc() { code $1 --touch-events; }
```
