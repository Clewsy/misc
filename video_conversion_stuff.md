# requires ffmpeg
```shell
$ sudo apt update && sudo apt install ffmpeg
```

# change container without re-encoding
``` shell
$ ffmpeg -i input.mp4 -codec copy output.mkv
```

- It auto-detects a Matroska to MP4 container conversion based on input/output filenames.
- "-codec copy" stream copies, or "re-muxes", the streams from the input to the output without re-encoding. Think of it like a copy and paste.
- Default stream selection behavior is to select only one stream per stream type. For example, if your input has two video streams and one audio stream then only the video stream with the largest frame size will be selected. Add -map 0 if you want to select all streams from the input.
- Some containers may not support some formats. So check if your chosen container format, be it mkv, mp4 or even avi has support for all the content in your files (video, audio, subtitles, data, etc). For example, mp4 does not support SubRip subtitles (.srt files).


# actually reduce file size
```shell
$ ffmpeg -i input.mp4 -vcodec libx264 -crf 20 output.mp4
```

# h.265
Nowadays (2020) a video format much better than H.264 is widely available, namely H.265 (better in that it compresses more for the same quality, or gives higher quality for the same size).

To use it, replace the libx264 codec with libx265, and push the compression lever further by increasing the CRF value — add, say, 4 or 6, since a reasonable range for H.265 may be 24 to 30.  For example:
```shell
$ ffmpeg -i input.mp4 -vcodec libx265 -crf 26 output.mp4
```

# rotate  a video
```shell
$ ffmpeg -i in.mov -vf "transpose=1" out.mov
```
Use	"transpose=0"	for 90deg counter-clockwise and vertical flip.
Use	"transpose=1"	for 90deg clockwise.
Use	"transpose=2"	for 90deg counter-clockwise.
Use	"transpose=3"	for 90deg clockwise and vertical flip.

# trim/cut seconds out of a video
```shell
$ ffmpeg -i input.mp4 -ss 00:00:10 -to 00:01:00 -c copy output.mp4
```

# convert a 1080p video to 720p
```shell
$ ffmpeg -i input.mkv -s hd720 -c:v libx26666665 -crf 23 -c:a aac -strict -2 output.mkv
```
