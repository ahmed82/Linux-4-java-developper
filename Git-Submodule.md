git submodule add -b develop <URL>

git submodule add -b develop  <URL>

git submodule init
git submodule update

git clone --recursive //Cloning a repository that contains submodules

If you already have cloned a repository and now want to load it’s submodules you have to use submodule update.

git submodule update --init
# if there are nested submodules:
```
git submodule update --init --recursive
```

# pull all changes in the repo including changes in the submodules
```
git pull --recurse-submodules
```

# pull all changes for the submodules
```
git submodule update --remote
```


2. Cloning a repository that contains submodules
If you want to clone a repository including its submodules you can use the --recursive parameter.
```
git clone --recursive 
```
