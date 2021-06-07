# Git cmd cheatsheet 

to checkout a specific commit hash
```
git checkout -b <new_branch_name> <sha1>
```
# Git Log
## Short list of 5 commit from the log 
```
git log --oneline -n 5
```
The --oneline flag condenses each commit to a single line.
--decorate flag makes git log display all of the references (e.g., branches, tags, etc) that point to each commit.
--decorate will format the commit history
The --graph option draws an ASCII graph representing the branch structure of the commit history. This is commonly used in conjunction with the --oneline and --decorate commands to make it easier to see which commit belongs to which branch:
```
git log --oneline -n 5
git log --graph --decorate --oneline
git log --after="2014-7-1"
git log --after="yesterday"
git log --after="2014-7-1" --before="2014-7-4"
Note that the --since and --until flags are synonymous with --after and --before, respectively.
```
### By Author
```
git log --author="John"
git log --author="John\|Mary"
git reset --hard HASH-CODE
```
### By Message
```
git log --grep="JRA-224:"
```
### By File
```
git log -- foo.py bar.py
```
The -- parameter is used to tell git log that subsequent arguments are file paths and not branch names. If there’s no chance of mixing it up with a branch, you can omit the --.
### By Range
This command is particularly useful when you use branch references as the parameters. It’s a simple way to show the differences between 2 branches. Consider the following command:
```
git log master..feature
```
```
git log --no-merges
```
### On the other hand, if you’re only interested in the merge commits, you can use the --merges flag:
```
git log --merges
```
## Link the deattached Head
```
git reset --hard HASH-CODE
```
## Graphical view of the project history
```
gitk --all
```

# Git Reset
## Revert one committ back 
```
git reset --soft HEAD~1
git reset HEAD~1 // tested on loyalty-Solution Master
```
If you don't want to keep these changes, simply use the --hard flag. Be sure to only do this when you're sure you don't need these changes anymore.
```
git reset --hard HEAD~1
```
`Note: if the reset not working delete every file from the git index by using:
```
git rm --cached -r .
```
## View log in one line
```
git log --graph --decorate --oneline
```
