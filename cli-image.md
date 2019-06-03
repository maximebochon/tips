# Command line image and document handling and processing tips

Timeshift by one hour [EXIF](https://en.wikipedia.org/wiki/Exif) dates of [JPEG](https://jpeg.org/jpeg/) pictures using [ExifTool](http://owl.phy.queensu.ca/~phil/exiftool/):
```sh
exiftool "-AllDates+=0:0:0 1:0:0" *.jpg
```

&nbsp;

Rename [JPEG](https://jpeg.org/jpeg/) pictures based on [EXIF](https://en.wikipedia.org/wiki/Exif) information using [ExifTool](http://owl.phy.queensu.ca/~phil/exiftool/):
```sh
exiftool -dateFormat %Y-%m-%d_%Hh%Mm%Ss '-Filename<Cuba.${DateTimeOriginal}${SubSecTimeOriginal;$_=substr($_,0,3);$_.=0 x(3-length)}.${Model;tr/ /-/}.%e' *.jpg
# example: IMG_1042.jpg --> Cuba.2019-03-12_10h55m36s002.Canon-EOS-50D.jpg
#          IMG_2658.jpg --> Cuba.2019-03-29_17h29m44s432.Redmi-Note-6-Pro.jpg
```

&nbsp;

Copy [EXIF](https://en.wikipedia.org/wiki/Exif) information from one picture to another using [ExifTool](http://owl.phy.queensu.ca/~phil/exiftool/):
```sh
exiftool -TagsFromFile source.jpg target.jpg
```

&nbsp;

Reencode a [JPEG](https://jpeg.org/jpeg/) image to change its quality using [ImageMagick](https://www.imagemagick.org/):
```sh
convert input.jpg -quality $quality output.jpg 
# quality from 1 to 100
```

&nbsp;

Resize image using [ImageMagick](https://www.imagemagick.org/):
```sh
convert $input -resize ${width} $output
convert $input -resize x${height} $output
convert $input -resize ${percentage}% $output
convert $input -resize ${width}x${height} $output
```

&nbsp;

Assemble images as a mosaic using [ImageMagick](https://www.imagemagick.org/):
```sh
montage -mode concatenate -tile 4x3 *.png out.png
```

&nbsp;

Assemble images as a photo board using [ImageMagick](https://www.imagemagick.org/):
```sh
montage -verbose -auto-orient -geometry 160x160+2+2 -tile 6x4 \
        -fill 'gray' -background 'black' -title 'My Photo Board' \
        ./photos/*.jpg board.jpg
```

&nbsp;

Render a multi-page [PDF](https://en.wikipedia.org/wiki/PDF) document to high-quality [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) images using [GhostScript](https://www.ghostscript.com/):
```sh
gs -sDEVICE=png16m -r600 -dDownScaleFactor=3 \   # 600/3 = 200 DPI (adjust to your need)
   -dTextAlphaBits=4 -dGraphicsAlphaBits=4 \     # best anti-aliasing setting in GhostScript
   -o ${output}.%d.png ${input}.pdf              # page number is part of the output file name
```

&nbsp;

Combine multiple size [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) images into one [icon file](https://en.wikipedia.org/wiki/ICO_%28file_format%29) using [ImageMagick](https://www.imagemagick.org/):
```sh
convert icon-{16,32,48,256}px.png icon.ico
```

&nbsp;

Split a multi-page [PDF](https://en.wikipedia.org/wiki/PDF) document into multiple one-page [PDF](https://en.wikipedia.org/wiki/PDF) documents using [QPDF](http://qpdf.sourceforge.net/):
```sh
qpdf --split-pages input.pdf output-%d.pdf
# %d is replaced with the page number
```

&nbsp;

Extract some pages from a [PDF](https://en.wikipedia.org/wiki/PDF) document into a new [PDF](https://en.wikipedia.org/wiki/PDF) document using [QPDF](http://qpdf.sourceforge.net/):
```sh
qpdf --empty --pages input.pdf 2-4,7 -- output.pdf
# extract pages 2, 3, 4, 7 from input.pdf into output.pdf
```

&nbsp;

Merge multiple [PDF](https://en.wikipedia.org/wiki/PDF) documents using [QPDF](http://qpdf.sourceforge.net/):
```sh
qpdf --empty --pages a.pdf b.pdf c.pdf -- abc.pdf
# merge a.pdf, b.pdf, c.pdf into abc.pdf
```