# Where to copy font files
For ubuntu copy *.ttf file to: `/usr/local/share/fonts/truetype/.`

# Change console font size for monitor connected to headless system

## Temporary:
```shell
$ ## check /usr/share/consolefonts for available fonts
$ fontsize /usr/share/consolefonts/Arabic-VGA-32x16.psf.gz
```

## Permanent (survive power cycle)
``` shell
$ sudo dpkg-reconfigure console-setup
```

- Encoding to use on the console: UTF-8
- Character set to support: Arabic
- Font for the console: VGA
- Font size: 16x32
- Alternatively, DejaVu 16x30 is a good option.

