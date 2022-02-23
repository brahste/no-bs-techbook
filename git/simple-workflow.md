# Git Simple Workflow

To begin, clone the repository you need to work on
```bash
git clone git@gitlab.com:<project-name>/<repo-name>.git
```

If the repo is already cloned locally then update the `master`/`main` branch with remote changes
```bash
git checkout master
git pull
```

Next, create the branch that will be used to develop, iterate, and test changes
```bash
git checkout -b <name-of-your-branch>
```

Once you've made a few changes stage the new code to be committed
```bash
git add .
```
(You may want to specify which files to stage explicitly instead of using the `.` catchall.)

Ensure the code you've staged compiles and that all of the tests are passing. Depending on the way you've set up your build this may look something like
```bash
./run // e.g. a bash script that standardizes the build with cmake etc.
./build/unittests
```

If everything is working well, update the version number in the top-level `CMakeLists.txt`, then stage the change and commit.
```bash
git add CMakeLists.txt
git commit -m "A descriptive message"
```

After a few commits and your code is ready, push your commits to the remote repo (do this often, especially if you use CI/CD, to catch build and test issues)
```bash
git push -u origin <name-of-your-branch>
```
This will set the remote repo to `origin` and push your branch to it. The `-u` option only has to be used on the first push to specify where the upstream branch at the remote location The `-u` option only has to be used on the first push to specify where the upstream branch at the remote location.

Once you've completed all the pushes and merged the branch into master, you can clean your repo by removing the remote and local branches that are no longer needed.
```bash
git pull -p
git branch -d <branch-name>
```

The first of the two commmands above _prunes_ the repo, removing any remote branches that were merged and deleted on the source control portal (e.g. GitLab). The second command removes the local branch.



