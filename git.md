## Git cmd cheatsheet 

to checkout a specific commit hash
```
git checkout -b <new_branch_name> <sha1>
```
## Short list of 5 commit from the log 
```
git log --oneline -n 5
```

## to link the deattached Head
```
git reset --hard HASH-CODE
```
### graphical view of the project history
```
gitk --all
```

### Go back one committ back 
```
git reset --soft HEAD~1
```
If you don't want to keep these changes, simply use the --hard flag. Be sure to only do this when you're sure you don't need these changes anymore.
```
git reset --hard HEAD~1
```

## View log in one line
```
git log --graph --decorate --oneline
```
