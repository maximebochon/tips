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
  - enable PDF operations in ImageMagick

* Audio tips:
  - choose MP3 compression bitrate and quality
  - Compresser en AAC CBR avec FFMpeg sans bibliothèque additionnelle : `ffmpeg -i input.wav -c:a aac -b:a 160k output.m4a`

* Windows tips:
  - check uptime command, and add alternative command using `systeminfo`

* Linux tips:
  - simpler alternative command to finding text in files using grep with some options?
  - XFCE: add type-related send-to commands in file manager
  - `sudo groupadd restricted`, `sudo usermod -aG restricted jdoe`, `id jdoe`
  - `sudo chown root:root /home/jdoe`, `sudo chmod 755 /home/jdoe`, `sudo chown jdoe:jdoe sub_dir`

* SFTP basics : `get [-r]`, `put [-r]`, `rm`, `rename`, `ls`, `pwd #remote`, `lcd #local`, `lpwd #local`, `!<local_command>` `exit`

* Java 8:
  - `list.stream().anyMatch(Objects::isNull)`
  - `pathList.sort(Path::compareTo)`;

* CLI general:
  - check POSIX compliance of cli-general
  - strace basics
  - Remplacer les retours à la lignes Windows par : `cat file | tr "\r\n" "##"`
  - Exemple de substitution en perl vers la sortie standard : `perl -p -e 's/parent\.VARIABLES\.(\w+)/parent.VARIABLES.X.$1/g' file > file2`
  - Exemple de substitution en perl avec remplacement sur place : `perl -pi.bak -e 's/parent\.VARIABLES\.(\w+)/parent.VARIABLES.X.$1/g' file`
  - Extraction des lignes contenant `parent.VARIABLES` dans tous les .html : `find . -name "*.html" | xargs grep "parent.VARIABLES" | sed -e 's/html:/~/' | cut -d~ -f2- | sort -u`
  - Liste des fichiers .html contenant `parent.VARIABLES` : `find . -name "*.html" | xargs grep parent.VARIABLES | cut -d: -f1 | sort -u`
  - Ajouter une ligne "toto" avant chaque ligne "tata" : `perl -ni.bak -e 'print "toto\n" if $_ =~ /tata/; print;' file`
  - Ajouter une ligne "toto" avant la premiere ligne "tata" : `perl -ni.bak -e 'BEGIN{$c=0} print "toto\n" if $_ =~ /tata/ and 0 == $c++; print;' file`

* VIM basics:
  - `:`, `/`, `n`, `:$`, `$`, `R`, `r`, `D`, `dd`, `C`, `o`, `:q`, `:wq`, :`q!`

* Facebook:
  - insert an empty first line in a comment : insert a _soft hyphen_ (`&#173;`) just before the carriage return

* XML ?
  - `xmllint --xpath "//*[local-name()='stage']/@name" $f 2>/dev/null`
  - `xmllint --format document.xml`

* Windows:
  - install Ubuntu via WSL 2 : PS> wsl --install Ubuntu
  - install Windows Terminal without having access to the Windows Store
  - set default terminal in Windows Terminal 
  - add GitBash profil into Windows Terminal
  - GitBash cygpath

* Kubernetes:
  - `k get <kind> --show-labels`, `k get CiliumNetworkPolicy`
  - `k delete <kind> <name> -n <namespace>`
  - `k get account <account>`
  - `helm list -n <namespace>`

* Git tips:
  - 

```sh
### Delete untracked files ###

git clean --dry-run # files are not deleted for real
# ...

git clean -f # files are deleted straightaway
# ...

git clean -i # interactive: git asks for what to do
# ...
```

```sh
### Start an interactive rebase session ###

git rebase -i HEAD~$N
# explain
```
