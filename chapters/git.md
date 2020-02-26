# Git

### Q: How to list branches in Git?

```sh
# Show list of local branches and highlight a current working branch
git branch
# Show all branches in local and remote repositories
git branch -a
# Show only remote branches
git branch -r
```

### Q: How to find merged/unmerged branches in git?

```sh
# all merged
git branch --merged master
# all not merged yet
git branch --no-merged master
# or all local and remote
git branch -r --no-merged origin/master
```
Source: [StackOverflow](https://stackoverflow.com/a/12276041/718722)

### Q: How to remove local (untracked) files from the current Git working tree?

```sh
# Print out the list of files which will be removed (dry run)
git clean -n
# Delete the files from the repository
git clean -f
# Remove untracked files, including directories (-d) and files ignored by git (-x)
git clean -d -x -f
```
Source: [StackOverflow](https://stackoverflow.com/a/64966/718722)

Alternative solution:
```sh
# Discard uncommitted changes in a specific file
git checkout thefiletoreset.txt
# To reset the entire repository to the last committed state
git reset --hard
```
Source: [StackOverflow](https://stackoverflow.com/a/675797/718722)
