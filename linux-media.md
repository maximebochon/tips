# Linux Media Handling tips

Convert audio file to Ogg-Vorbis, FLAC or LAME-MP3:
```sh
sox ${input_audio} -C ${quality} ${output_audio}.ogg
# Ogg-Vorbis quality from -1 (worst) to 10 (best)

sox ${input_audio} -C ${compression_level} ${output_audio}.flac
# FLAC compression level from 0 (low) to 8 (high)

sox ${input_audio} -C 320.0 ${output_audio}.mp3
# LAME-MP3 constant bitrate of 320 kbps at best quality
```

&nbsp;

Timeshift by one hour EXIF dates of JPEG pictures:
```sh
exiftool "-AllDates+=0:0:0 1:0:0" *.jpg
```

&nbsp;

Rename JPEG pictures based on EXIF information:
```sh
exiftool -dateFormat %Y-%m-%d_%Hh%Mm%Ss '-Filename<Cuba.${DateTimeOriginal}_${SubSecTimeOriginal;$_.=0 x(3-length)}.${Model;tr/ /-/}.%e' *.jpg
# example: IMG_0123.jpg --> Cuba.2019-03-12_10h55m36s722.Canon-EOS-50D.jpg
```

&nbsp;

Copy EXIF information from one picture to another:
```sh
exiftool -TagsFromFile source.jpg target.jpg
```

&nbsp;

Merge Matroska videos:
```sh
mkvmerge -o output.mkv input1.mkv \+ input2.mkv \+ input3.mkv
```

&nbsp;

Reencode a JPEG image to change its quality:
```sh
convert input.jpg -quality $quality output.jpg 
# quality from 1 to 100
```

&nbsp;

Assemble images as a mosaic using ImageMagick:
```sh
montage -mode concatenate -tile 4x3 *.png out.png
```

&nbsp;

Assemble images as a photo board using ImageMagick:
```sh
montage -verbose -auto-orient -geometry 160x160+2+2 -tile 6x4 \
        -fill 'gray' -background 'black' -title 'My Photo Board' \
        ./photos/*.jpg board.jpg
```
