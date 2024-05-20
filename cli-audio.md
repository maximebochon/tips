# Command line audio handling and processing tips

:recycle: Convert one audio file to [Ogg](https://xiph.org/ogg/)-[Vorbis](https://xiph.org/vorbis/), [FLAC](https://xiph.org/flac/) or [LAME-MP3](http://lame.sourceforge.net/) using [SoX](http://sox.sourceforge.net/):
```sh
sox ${input_audio} -C ${quality} ${output_audio}.ogg
# Ogg-Vorbis quality from -1 (worst) to 10 (best)
# Quality factor:  -1   0   2    4    6    8    9   10
# Bitrate (kbps):  45  64  96  128  192  265  320  500

sox ${input_audio} -C ${compression_level} ${output_audio}.flac
# FLAC compression level from 0 (low) to 8 (high)

sox ${input_audio} -C 320.0 ${output_audio}.mp3
# LAME-MP3 constant bitrate of 320 kbps at best quality
```

&nbsp;

:recycle: Convert all files in current directory to another format using [SoX](http://sox.sourceforge.net/):
```sh
# Convert all WAVE files to FLAC
for file in *.wav; do sox "$file" "${file%.*}".flac; done

# Convert all FLAC files to MP3 (256 kbps, best encoding quality)
for file in *.flac; do sox "$file" -C 256.0 "${file%.*}".mp3; done
```

&nbsp;

:recycle: Convert one audio file to constant bitrate [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding) using [FFmpeg](https://ffmpeg.org/):
```sh
ffmpeg -i ${input_audio} -c:a aac -b:a ${bitrate}k ${output_audio}.m4a
```
More options are described [here](https://trac.ffmpeg.org/wiki/Encode/AAC).

&nbsp;

:oden: Concatenate audio files losslessly using [FFmpeg](https://ffmpeg.org/) (more information [here](https://trac.ffmpeg.org/wiki/Concatenate)):
- create a text file `concat-list.txt` to describe files to be concatenated:
```
file 'relative-path-to-file-1.m4a'
file 'relative-path-to-file-2.m4a'
file '/absolute/path/to/file-3.m4a'
```
- use the following FFmpeg command:
```sh
ffmpeg -f concat -i concat-list.txt -c copy output.m4a
```

&nbsp;

:scissors: Extract a part of an AAC audio file losslessly using [FFmpeg](https://ffmpeg.org/):
```sh
ffmpeg -i input.m4a -c:a copy -ss ${start} -t ${duration} part.m4a
ffmpeg -i input.m4a -c:a copy -ss ${start} -to ${end} part.m4a
# start, duration and end are written this way: HH:MM:SS.sss
# (HH: hours, MM: minutes, SS: seconds, sss: milliseconds)
```
