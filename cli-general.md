# General command line tips

:open_file_folder: Create a compressed archive **and** remove archived files **in one** command line:
```sh
tar --remove-files -czf archive.tar.gz *.ext
```

&nbsp;

:arrows_counterclockwise: Display the result of a command and update/refresh it every *PERIOD* seconds:
```sh
PERIOD=2;         # update period (in seconds)
while [ 1 ];      # infinite loop
  do tput clear;  # clear the content of the terminal
  date;           # any quick command displaying information
  sleep $PERIOD;  # wait for PERIOD seconds
done
```
Works well as a one-liner too:
```sh
while [ 1 ]; do tput clear; date; sleep 2; done
```
...but even better, there is an app for that!
```sh
watch -n $PERIOD date
```

&nbsp;

:link: Display the absolute path to an executable command *cmd*:
```sh
readlink -f $(which $cmd)
```
Example:
```sh
which mvn
# /usr/bin/mvn
readlink -f $(which mvn)
# /usr/local/apache-maven-3.2.5/bin/mvn
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

&nbsp;

:bar_chart: Group and count text occurrences:
```sh
# Create a list of occurrences

for x in a b a c b b b a c a c a a b a; do
  echo $x | sed -e 's/a/Apple/' -e 's/b/Banana/' -e 's/c/Cherry/'
done > list

head -5 list
# Apple
# Banana
# Apple
# Cherry
# Banana

wc -l list
# 15
```
```sh
# Group and count occurrences

cat list | sort | uniq -c
#      7 Apple
#      5 Banana
#      3 Cherry
```

&nbsp;

:1234: Compute basic metrics on a list of integers:
```sh
# Let's consider a file named 'unsorted-integers'
# containing unsorted integers (one integer per line).

sort -n unsorted-integers > sorted-integers; INPUT="sorted-integers"

echo "Min="$(head -1 $INPUT); \
echo "Max="$(tail -1 $INPUT); \
awk '{sum += $1} END {print "Count="NR; print"Total="sum; print "Average="sum/NR}' $INPUT

# Min=2861
# Max=110403
# Count=206
# Total=53591
# Average=15609
```

&nbsp;

:family: Find everything owned by a user or a group:
```
sudo find / -user $USER
sudo find / -group $GROUP
```

&nbsp;

:skull: Delete a user or a group:
```
sudo userdel $USER
sudo groupdel $GROUP
```

&nbsp;

:heavy_division_sign: Fun code to delete one file out of two (unsafe for file names with spaces):
```sh
for f in *.xml; do [ -f rm ] && rm -f $f && rm rm || touch rm; done; rm -f rm;
```

&nbsp;

:ghost: Prevent commands in a `bash` terminal from being stored in history:
- `HISTCONTROL` environment variable should be set to `ignorespace` or `ignoreboth` (done by default on most systems)
- type your command with a leading space to prevent storing it in history

&nbsp;

:closed_lock_with_key: Encrypt and decrypt a file by passphrase using [GNU Privacy Guard](https://gnupg.org/):
```sh
gpg --output data-file.encrypted --symmetric --cipher-algo AES256 data-file
gpg --output data-file.decrypted --decrypt data-file.encrypted
# cksum on data-file.decrypted should give same result as on data-file
```

&nbsp;

:alarm_clock: Display and schedule jobs using [`crontab`](https://en.wikipedia.org/wiki/Cron):

```sh
# Display scheduled jobs for the current user:
crontab -l

# Display scheduled jobs for the specified user:
crontab -u ${some_user} -l

# Display scheduled jobs if crontab is not allowed:
(sudo) cat /var/spool/cron/crontabs/${some_user}

# Edit scheduled jobs for the current user:
crontab -e
```
```sh
# Run a script every working day, every hour, from 8 AM to 8 PM
0 8-20 * * 1-5 bash -c "/opt/some-script.sh"

# Start some service every day at 8 AM, stop it at 11 PM
0    8 * * * bash -c "/opt/some-service.sh start"
0   23 * * * bash -c "/opt/some-service.sh stop"
```
