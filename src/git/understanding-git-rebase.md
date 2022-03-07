# Understanding Git Rebase

Links:
- https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase
- https://www.atlassian.com/git/tutorials/merging-vs-rebasing

Rebasing is the process of integrating a sequence of commits into a new base commit. The idea behind rebasing is similar to when a branch is created. When you create a branch you diverge from a base commit (often `main`); by rebasing you change your commit change to appear as if you had branched from a different base commit than originally used.

One of the main reasons for rebasing si to maintain a clean commit history. In the end this makes regressions and bug-finding easier.

__Never rebase commits once they've been pushed to a public repository__

One issue with rebasing is that it can cause many merge conflicts in the process of rebasing. This can be remedied by rabsing your branch frequenclt againt `main` and making more frequent commits. 
