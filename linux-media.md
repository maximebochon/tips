# Linux Media Handling tips

Convert audio file to [Ogg](https://xiph.org/ogg/)-[Vorbis](https://xiph.org/vorbis/), [FLAC](https://xiph.org/flac/) or [LAME-MP3](http://lame.sourceforge.net/) using [SoX](http://sox.sourceforge.net/):
```sh
sox ${input_audio} -C ${quality} ${output_audio}.ogg
# Ogg-Vorbis quality from -1 (worst) to 10 (best)

sox ${input_audio} -C ${compression_level} ${output_audio}.flac
# FLAC compression level from 0 (low) to 8 (high)

sox ${input_audio} -C 320.0 ${output_audio}.mp3
# LAME-MP3 constant bitrate of 320 kbps at best quality
```

&nbsp;

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

Merge [Matroska](https://www.matroska.org/) videos using [MKVToolNix](https://mkvtoolnix.download/):
```sh
mkvmerge -o output.mkv input1.mkv \+ input2.mkv \+ input3.mkv
```

&nbsp;

Apply geometric transformations to a video with relative values using [FFmpeg](https://ffmpeg.org/):
```sh
ffmpeg -i $input -vf "rotate=PI,crop=2/3*in_w:3/4*in_h:0:1/4*in_h" $output
# rotate by 180 degrees and crop as follows:
#   horizontal position: 0
#   vertical position: 1/4 of original height
#   new width: 2/3 of original width
#   new height: 3/4 of original height
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

Combine multiple size [PNG](https://en.wikipedia.org/wiki/PDF) images into one [icon file](https://en.wikipedia.org/wiki/ICO_%28file_format%29) using [ImageMagick](https://www.imagemagick.org/):
```sh
convert icon-{16,32,48,256}px.png icon.ico
```
