# Linux tips

Create a compressed archive **and** remove archived files **in one** command line:
```sh
tar --remove-files -czf archive.tar.gz *.ext
```

Display the result of a command and update/refresh it every *S* seconds:
```
S=1;             # update period, in seconds
while [ 1 ];
  do tput clear; # clear the content of the terminal
  date;          # any quick command displaying information
  sleep $S;      # wait for S seconds
done
```
Works well as a one-liner too:
```
while [ 1 ]; do tput clear; date; sleep 1; done
```

Display the absolute path to an executable command *cmd*:
```sh
readlink -f $(which $cmd)
```
Example:
```sh
which mvn
-- /usr/bin/mvn
readlink -f $(which mvn)
-- /usr/local/apache-maven-3.2.5/bin/mvn
```
