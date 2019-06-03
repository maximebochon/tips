* Image/doc tips:
  - lossless JPEG cropping
  - lossless JPEG rotating (`jpegtran -rotate 90 -perfect input.jpg > output.jpg`)
  - `convert -page A5 input.jpg output.pdf, convert -rotate 270 input.pdf output.pdf`
  - pdfsandwich
  - how to install jpegtran: `sudo apt install libjpeg-progs`
  - `montage image{1,2,3}.png -tile 1x3 -geometry +0+0 images.png`

* Audio tips:
  - choose MP3 compression bitrate and quality

* Windows tips:
  - check uptime command, and add alternative command using `systeminfo`

* Linux tips:
  - simpler alternative command to finding text in files using grep with some options?

* Java 8:
  - `list.stream().anyMatch(Objects::isNull)`
  - `pathList.sort(Path::compareTo)`;
  
* CLI general:
  - check POSIX compliance of cli-general
