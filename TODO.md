# TODO List

* Image/doc tips:
  - lossless JPEG cropping
  - lossless JPEG rotating (`jpegtran -rotate 90 -perfect input.jpg > output.jpg`)
  - `convert -page A5 input.jpg output.pdf`
  - pdfsandwich
  - how to install jpegtran: `sudo apt install libjpeg-progs`
  - `montage image{1,2,3}.png -tile 1x3 -geometry +0+0 images.png`
  - `mogrify ... *.png`
  - `djvudigital`
  - `pdf2djvu`
  - `jbig2dec`
  - `http://www.cheapimpostor.com/PDFInspector/`
  - `pdfimages -list input.pdf`
  - `pdfimages -all input.pdf prefix`
  - `pdfimages -png input.pdf prefix`
  - `pdfinfo input.pdf`
  - `qpdf --stream-data=uncompress compressed.pdf uncompressed.pdf`
  - `qpdf uncompressed.pdf compressed.pdf`
  - `qpdf --qdf --object-streams=disable in.pdf out.pdf`

* Audio tips:
  - choose MP3 compression bitrate and quality

* Windows tips:
  - check uptime command, and add alternative command using `systeminfo`

* Linux tips:
  - simpler alternative command to finding text in files using grep with some options?
  - XFCE: add type-related send-to commands in file manager
  - get GUI program PID by clicking on its window via `xprop`

* Java 8:
  - `list.stream().anyMatch(Objects::isNull)`
  - `pathList.sort(Path::compareTo)`;
  
* CLI general:
  - check POSIX compliance of cli-general

* Facebook:
  - insert an empty first line in a comment : insert a _soft hyphen_ (`&#173;`) just before the carriage return

* XML ?
  - `xmllint --xpath "//*[local-name()='stage']/@name" $f 2>/dev/null`
  - `xmllint --format document.xml`
