# Command line video handling and processing tips

:dango: Concatenate consecutive video parts using [MKVToolNix](https://mkvtoolnix.download/):
```sh
mkvmerge -o output.mkv input1.mkv \+ input2.mkv \+ input3.mkv
mkvmerge -o full.mkv part1.avi \+ part2.avi
mkvmerge -o abc.mp4 a.mp4 \+ b.mp4 \+ c.mp4
```

&nbsp;

:triangular_ruler: Apply geometric transformations to a video with relative values using [FFmpeg](https://ffmpeg.org/):
```sh
ffmpeg -i $input -vf "rotate=PI,crop=2/3*in_w:3/4*in_h:0:1/4*in_h" $output
# rotate by 180 degrees and crop as follows:
#   horizontal position: 0
#   vertical position: 1/4 of original height
#   new width: 2/3 of original width
#   new height: 3/4 of original height
```

&nbsp;

:gift: Change media container type without reencoding using [FFmpeg](https://ffmpeg.org/):
```sh
ffmpeg -i video.mov -codec copy video.mp4
ffmpeg -i video.mp4 -codec copy video.mkv
...
```
