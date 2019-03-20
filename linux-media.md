# Linux Media Handling tips

Convert audio file to Ogg format and Vorbis codec:
```sh
sox ${input_audio} -C ${quality} ${output_audio}.ogg
# quality from -1 (worst) to 10 (best)
```


Convert audio file to FLAC format and codec:
```sh
sox ${input_audio} -C ${compression_level} ${output_audio}.flac
# compression level from 0 (low) to 8 (high)
```


Convert audio file to (LAME) MP3 format and codec:
```sh
sox ${input_audio} -C 320.0 ${output_audio}.mp3
# constant bitrate of 320 kbps at best quality
```
