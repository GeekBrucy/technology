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