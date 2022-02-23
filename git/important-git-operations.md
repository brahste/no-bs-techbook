# Important Git Operations 

Below, typically `<remote-name> == origin`
## Getting info on remote changes
```
git fetch <remote-name>
```

## Merging (remote) changes into a local branch
```
git merge <remote-name>/<branch-name>
```
Note that `git merge` can also be used to merge local branches together. In this case the branch that is specified is merged _into_ the branch that is currently "checked out"
```
git checkout feature-branch
git merge main
```
The above operation will merge `main` into `feature-branch`


## Creating a local branch from an existing remote branch

```
git checkout --track <remote-name>/<branch-name>
```

If you want the local branch to have a different name than the remote branch then you can use
```
git remote add <remote-name> <repo-url>
git fetch <remote-name>
git checkout -b <local-branch-name> <remote-name>/<branch-name>
```

## Reversing a merge

To reverse a merge to the commit directly before the merge occured
```
git reset --merge ORIG_HEAD
```

To reverse to a specific commit
```
git reset --merge <commit-sha>
```

## Deleting local branch once remote branch is merged and deleted

When working with a source control UI like GitHub or GitLab, often the UI will allow you to merge remote feature branches with `main` and then automatically delete them. In this case you may still have lingering local branches that would be best to clean up.

First prune any remote changes
```
git fetch <remote-name> -p    // short for --prune
```
This will remove any remote branches that have been deleted.

Next, make sure you're ahead of the branch you merged
```
git checkout main
git merge origin/main
git branch -d <branch>    // short for --delete
```
