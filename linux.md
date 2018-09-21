# Linux tips

:open_file_folder: Create a compressed archive **and** remove archived files **in one** command line:
```sh
tar --remove-files -czf archive.tar.gz *.ext
```

&nbsp;

:arrows_counterclockwise: Display the result of a command and update/refresh it every *S* seconds:
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

&nbsp;

:link: Display the absolute path to an executable command *cmd*:
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

&nbsp;

:mag: List all files containing some text:
```sh
find . -type f -exec grep -H <some_text> {} \; 2>/dev/null | cut -d':' -f1 | sort -u
```
Explanation:
```sh
# Find all files recursively in current directory.
find . -type f \
# For each file, search for <some_text> and format
# results this way: <file_name>:<matched_line>
-exec grep -H <some_text> {} \; \
# Ignore permission issues.
2>/dev/null \
# Filter on file names.
| cut -d':' -f1 \
# Remove duplicates (and sort).
| sort -u
```

&nbsp;

:bookmark_tabs: Find some expression in a file and display surrounding lines:
```sh
grep -B 2 -A 5 $some_expression $file
# display lines where the expression was found
# surrounded with 2 previous lines (B = before)
# and 5 following lines (A = after)
```
