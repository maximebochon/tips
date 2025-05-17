# Command line video handling and processing tips

:dango: Concatenate consecutive video parts using [MKVToolNix](https://mkvtoolnix.download/):
```sh
mkvmerge -o output.mkv input1.mkv \+ input2.mkv \+ input3.mkv
mkvmerge -o full.mkv part1.avi \+ part2.avi
mkvmerge -o abc.mp4 a.mp4 \+ b.mp4 \+ c.mp4
```

&nbsp;

:abc: Combine consecutive [`.ts`](https://en.wikipedia.org/wiki/MPEG_transport_stream) files as one video using [FFmpeg](https://ffmpeg.org/):
```sh
cat 0001.ts 0002.ts 0003.ts > combined.ts
ffmpeg -i combined.ts -codec copy video.mp4
```
<!-- try the piped version 'cat ... | ffmpeg -i pipe:0 ...' -->

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

&nbsp;

:cyclone: Set orientation of [MOV](https://en.wikipedia.org/wiki/QuickTime_File_Format), [MP4](https://en.wikipedia.org/wiki/MPEG-4) and [3GP](https://fr.wikipedia.org/wiki/3GP) video files without reencoding using [FFmpeg](https://ffmpeg.org/):
```sh
ffmpeg -i input.$EXT -c copy -metadata:s:v:0 rotate=$ANGLE output.$EXT
# EXT: mov, mp4, 3gp
# ANGLE: 0, 90, 180, 270 (degrees)
```

&nbsp;

:loud_sound: Extract the audio track of a video using [FFmpeg](https://ffmpeg.org/):
```sh
# for editing purpose: audio is encoded uncompressed in WAVE format
ffmpeg -i video.mp4 audio.wav

# for storage purpose: audio is extracted losslessly and is supposed to be AAC encoded
ffmpeg -i video.mp4 -vn -c:a copy audio.m4a
```

&nbsp;

:musical_score: Replace the audio track of a video using [FFmpeg](https://ffmpeg.org/):
```sh
ffmpeg -i video.mp4 -i audio.wav -c:v copy -map 0:v -map 1:a video-with-new-audio.mp4
# video is not reencoded, audio is encoded in AAC
```

&nbsp;

:mute: Remove audio from a video using [FFmpeg](https://ffmpeg.org/):
```sh
ffmpeg -i video-with-audio.mp4 -vcodec copy -an video-without-audio.mp4
```

&nbsp;

:arrow_lower_right: Reencode video stream in H264 to optimize file size, keeping audio stream as is, using [FFmpeg](https://ffmpeg.org/):
```sh
# Reencode video only, using default video quality settings:
ffmpeg -i video.mp4 -c:a copy default-quality-video-with-same-audio.mp4

# As of 2025, the previous command, using default settings, should be equivalent to the following, more explicit, command:
ffmpeg -i video.mp4 -c:a copy -c:v libx264 -preset medium -crf 23 default-quality-video-with-same-audio.mp4

# Reencode video only, using slighlty higher quality settings, at the expense of time:
ffmpeg -i video.mp4 -c:a copy -c:v libx264 -preset slow -crf 21 higher-quality-video-with-same-audio.mp4
```

&nbsp;

:white_square_button: Extract a specific frame/image from a video as a PNG/JPEG file using [FFmpeg](https://ffmpeg.org/):
```sh
# save frame as a lossless PNG file
ffmpeg -ss 00:00:05.01 -i video.ext -frames:v 1 -qscale:v 2 image.png

# save frame as lossy but high quality JPEG file
ffmpeg -ss 00:00:05.06 -i video.ext -frames:v 1 -qscale:v 2 image.jpg
```
&nbsp;

:curly_loop: Save an [M3U8](https://en.wikipedia.org/wiki/M3U#M3U8) based [HTTP Live Streaming](https://en.wikipedia.org/wiki/HTTP_Live_Streaming)
to an [MP4](https://en.wikipedia.org/wiki/MP4_file_format) file using [FFmpeg](https://ffmpeg.org/):
```sh
ffmpeg -protocol_whitelist file,http,https,tcp,tls,crypto -i index.m3u8 -c copy -bsf:a aac_adtstoasc stream.mp4
```
