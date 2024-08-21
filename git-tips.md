## How to make sure that a previously cloned repo becomes disconnected
cd into that repo (i.e. cd/xxx)
remove the .git/
```
rm -r ./git
```
re-initialize the main repo after cd back to main
```
git init
git add .
```


## Github push and pull conflict
### If original conflict is not identifed in VS code
Accept the changes and then git pull
### If original conflict visualization is lost
```
git merge --abort 
```

### If it is a file deleted conflict (something deleted by others)
```
git add [path_to_file]
```
or 
```
git rm [path_to_file]
```
then 
```
git push
```

## Create a initial repo
1) Create a repo 2) add a file (README or whatever) 3) clone the repo in local directory 4) add the files you want to commit.
