# sync with two remote

## Senario
Given two remotes with same project, one is developed, another is not. Now I want to update the undeveloped one

## Solution

### Reset remote url

```
git remote set-rul branch-name branch-url
```

### set upstream

```
git branch --set-upstream-to=[remote_name]/<branche> master
```

Then check status, you should have some information like 'Your branche have diverged, and have xx and xx different commits each...'

### git pull
There will be a a fatal message says 'refusing to merge unrelated histories'

### use git pull [remote_name] [branch_name] --allow-unrelated-histories

### resolve conflicts and push

# Discard changes

### All Changes

```
git reset --hard
```

# Find what branches the specific has

lists branches merged into master
```
git branch --merged master 
```
lists branches merged into HEAD (i.e. tip of current branch)
```
git branch --merged 
```

lists branches that have not been merged
```
git branch --no-merged 
```
By default this applies to only the local branches. The -a flag will show both local and remote branches, and the -r flag shows only the remote branches.

# Find specific commit

```
git log | grep <commit_id>
```

```
git branch --contains $COMMIT_ID
```