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

## Adding a remote repository

```
git remote add <remote-name> <repo-url>
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

## Reversing a commit

The following command will revert the current branch from the HEAD to the commit referenced by the *commit-sha*.

```
git revert --no-commit <commit-sha>..HEAD
```

To reverse a commit before its been pushed

```
git reset --soft HEAD~<N>
```

Where `<N>` is the number of commits relative to the current head you wish your reverse to point to.

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

## Deleting local and remote branch

```
git push -d <remote_name> <branch_name>     // deletes remote branch
git branch -d <branch_name>                 // deletes local branch
```

If this complains that the branch may not be complete merged, use the `-D` option. Use with caution.

## Remove file from index but leave on filesystem

> Link:
> 
> - [Git remove a file from a branch, keep it in the master - Stack Overflow](https://stackoverflow.com/questions/37422221/git-remove-a-file-from-a-branch-keep-it-in-the-master)
