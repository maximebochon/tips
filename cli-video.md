# Command line video handling and processing tips

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

