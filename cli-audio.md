# Command line audio handling and processing tips

Convert audio file to [Ogg](https://xiph.org/ogg/)-[Vorbis](https://xiph.org/vorbis/), [FLAC](https://xiph.org/flac/) or [LAME-MP3](http://lame.sourceforge.net/) using [SoX](http://sox.sourceforge.net/):
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

Concatenate audio files losslessly using [FFmpeg](https://ffmpeg.org/) (more information [here](https://trac.ffmpeg.org/wiki/Concatenate)):
- create a text file `concat-list.txt` to describe files to be concatenated :
```
file 'relative-path-to-file-1.m4a'
file 'relative-path-to-file-2.m4a'
file '/absolute/path/to/file-3.m4a'
```
- use the following FFmpeg command:
```sh
ffmpeg -f concat -i concat-list.txt -c copy output.m4a
```
