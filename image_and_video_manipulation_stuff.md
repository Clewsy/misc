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

Reduce image filesize by reducing image quality.
```shell
$ convert image.jpg -quality 80 smaller_image_size.jpg
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

# Using ffmpeg

Simple conversion from one format to another.
```shell
$ ffmpeg -i input_vid.mp4 output_vid.mkv
```
- Use option -sn to disable subtitles in output.
- Use option -an to disable audio in output.

Cut seconds out of a longer video.
```shell
ffmpeg -i input_vid.mp4 -ss 00:00:02 -to 00:00:05 -c copy output_vid.mp4
```

Remove audio from a video file.
```shell
$ ffmpeg -i vid_with_audio.mp4 -c copy -an vid_without_audio.mp4
```

Rotate video.
```shell
$ ffmpeg -i input.mp4 -vf "transpose=1" output.mp4
```
Where the value for transpose corresponds to the following:
- 0 = 90CounterCLockwise and Vertical Flip (default)
- 1 = 90Clockwise
- 2 = 90CounterClockwise
- 3 = 90Clockwise and Vertical Flip

