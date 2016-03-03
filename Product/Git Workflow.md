# Git Workflow

How we use git.

## Rebase > Merge

In general, we like avoiding merge commits to keep our history clean. This means that we avoid using `git merge`.

```bash
# Make sure we've pulled the latest master
$ git checkout master
$ git pull

# Rebase it onto our branch
$ git checkout my-branch
$ git rebase master
```
