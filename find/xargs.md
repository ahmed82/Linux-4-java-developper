# xargs
```
echo 'one two three' | xargs mkdir
```
```
find ./foo -type f -name "*.txt" -exec rm {} \; 
find /tmp -mtime +14 | xargs rm
```
```
time find . -type f -name "*.txt" -exec rm {} \;
0.35s user 0.11s system 99% cpu 0.467 total

time find ./foo -type f -name "*.txt" | xargs rm
0.00s user 0.01s system 75% cpu 0.016 total
```
```
find ./foo -type f -name "*.txt" | xargs rm
```
The -t option prints each command that will be executed to the terminal. This can be helpful when debugging scripts.
```
echo 'one two three' | xargs -t rm
```
The -p command will print the command to be executed and prompt the user to run it. This can be useful for destructive operations where you really want to be sure on the command to be run.
```
echo 'one two three' | xargs -p touch
```
Run multiple commands with xargs by using the -I flag. This replaces occurrences of the argument with the argument passed to xargs. The following echos a string and creates a folder.
```
cat foo.txt | xargs -I % sh -c 'echo %; mkdir %'
```

