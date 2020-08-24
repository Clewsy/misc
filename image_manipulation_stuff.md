# Using `convert` (part of imagemagick suite)

Reduce image size by 50%
```shell
$ convert image.jpg -resize 50% half_image.jpg
```

Scale to  fixed width, proportional height
```shell
$ convert image.jpg -resize 500x small_image.jpg
```

Rotate image 90 degrees
```shell
$ convert -rotate 90 image.jpg rotated_image.jpg
```

# Using exiftool
Install exiftool
```shell
$ sudo apt install libimage-exiftool-perl
```

View metadata (exif data).
```shell
$ exiftool image.jpg
```

Delete gps location data.
```shell
$ exiftool -gps:all= image.jpg
```

Delete all metadata.
```shell
$ exiftool -all= -overwrite_original image.jpg
```

Delete all metadata for all \*.jpg files within current directory.
```shell
$ exiftool -all= -r -overwrite_original -ext jpg .
```

Delete gps location data for all \*.jpg files within the current directory.
```shell
$ exiftool -gps:all= *.jpg
```
