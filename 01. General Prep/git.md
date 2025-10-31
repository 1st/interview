# Git Interview Refresh

Keep these branches, cleanup commands, and conceptual contrasts top of mind so you can speak confidently about Git workflows in interviews.

## Quick Refresh
- List and filter branches locally and across remotes when walking through repo discovery.
- Explain how you identify merged versus unmerged branches before cleanup.
- Know how to delete untracked files safely and when to fall back to selective resets.
- Contrast merge and rebase to show you can choose the right integration strategy.

## Command Snippets

### Listing branches
```sh
# Show local branches and highlight the current one
git branch
# Show local and remote branches
git branch -a
# Show remote branches only
git branch -r
```

### Checking merge status
```sh
# Branches already merged into master
git branch --merged master
# Branches not yet merged into master
git branch --no-merged master
# Remote branches not merged into origin/master
git branch -r --no-merged origin/master
```

### Cleaning untracked files
```sh
# Dry run: preview files to be removed
git clean -n
# Remove untracked files
git clean -f
# Remove untracked directories and ignored files
git clean -d -x -f
```

### Resetting working tree changes
```sh
# Discard changes in a single file
git checkout -- path/to/file
# Reset entire working tree to last commit
git reset --hard
```

## Interview Prompts
- Walk through when you would choose merge versus rebase in a team workflow. (See [Atlassian](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).)
- Explain how you clean up stale feature branches without losing work.
- Describe your process for recovering from an accidental force push or bad commit.

## Deep Dive Later
- [Advanced Git Tutorials](https://www.atlassian.com/git/tutorials/advanced-overview) by Atlassian for branching models, hooks, and rebase strategies.
