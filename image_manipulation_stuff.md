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

