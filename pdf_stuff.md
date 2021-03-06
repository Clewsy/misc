# Convert image file to pdf
use convert - part of the ImageMagick suite
```shell
$ convert image.jpg image.pdf
```

# Rotate then convert
```shell
$ convert -rotate 90 image.jpg image.pdf
```

# Rotate 90 degrees - requires pdftk
Don't use convert - it will first convert pdf to an image, rotate then convert back to a pdf
Rotate clockwise:
```shell
$ pdftk <input.pdf> cat 1-endright output <output.pdf>
```
## 1-endright:
- ```1``` - start at page 1
- ```end``` - finish at last page
- ```right``` - rotate to the right (90deg)

## Example:
```shell
$ pdftk schematic.pdf cat 1-endleft output schematic_rot.pdf
```
for counter-clockwise, change ```1-endright``` to ```1-endleft```

# Extract pages - requires pdftk
```shell
$ pdftk full-pdf.pdf cat 12-15 output outfile_p12-15.pdf
```

# Merge pages - requires pdftk
```shell
$ pdfunite in-1.pdf in-2.pdf in-n.pdf out.pdf
```
