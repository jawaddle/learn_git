# Notes on Git, GitHub, diff, patch

> ## *diff and patch*

Compare two files using diff:

```bash
diff -u old_file new_file > changes.diff 
patch old_file changes.diff # apply mods in changes.diff to old_file
```
Other programs to consider:

- wdiff: word by word rather than line by line compare
- meld: graphical diff
- kDiff3: graphical diff
- vimdiff: graphical diff

> ## git history

- Written by Linus Torvalds in 2005
- git-scm.com (source control management)
- Windows version: MinGW64 @ gitforwindevs.org - comes with bash like shell
- MinTTY - GUI/Git for Windows

```bash
git config -l      # lists config params like email, user
git init           # Creates a .git directory in CWD
git clone <URL>    # clone a repo and create a project directory and .git dir in CWD
git status         # gives list of modified and untracked files and anything to commit
git add <filename> # tell git to start tracking file in this repo
git commit         # commit staging area/added files to repo
git commit -m "Topic for git commit message" # to avoid editor
git log            # display git commit messages
git commit -a      # commit all tracked files without git add -- does not work on new files
git log -p         # shows patches / changes in a git log with paging mode
git show <ID>      # ID is the unique ID accompanying a given commit
git log --stat     # summary of changes in git history
git diff           # show diff -u like changes in tracked files prior to commit
git add -p         # shows changes and allows confirmation before adding
git diff --staged  # show diff on 'staged' ready to commit files
git rm <filename>  # stop tracking and remove file from git repo
git mv <old_filename> <new_filename>  # rename a file in a git repo; must follow with git commit
git checkout <filename>  # revert unstaged file to latest snapshot in repo
git checkout -p <filename> # change by change acceptance of latest snapshot rather than all
git add *  # stage all tracked files
git reset HEAD <filename> # unstage filename

### Amending commits
git commit --amend # will commit all new staged items but allow editing of message
                   # even if nothing in staging area
                   # do not use on public commits
### Avoid amending commits that have already been made public

git revert HEAD  # contains the reverse of prior bad commit - should amend message to explain
git log -p -2    # look at last two log entries in a diff format
```

Git uses the HEAD alias to represent the currently checked out snapshot of a project

> ## Ignoring files with .gitignore

```bash
echo .DS_STORE > .gitignore  # add MacOSX specific file to ingore list for commits
git add .gitignore  # if not already added
git commit -m "Add .gitignore preference"
```
## Tips on .gitignore

- https://www.freecodecamp.org/news/gitignore-what-is-it-and-how-to-add-to-repo/
- https://github.com/github/gitignore/blob/master/Python.gitignore

```bash
git branch  # list all the currently active branches
git branch <new-feature> # create new branch with name <new-feature>
git checkout <new-feature> # change active branch to the one named <new-feature>
git checkout -b <my_new_branch> # create and change to new branch in one go
git branch -d <new-feature> # deletes branch called <new-feature>, if unmerged, will warn

# so let's assume we want to merge in a <new-feature> branch into <master> branch
git checkout master # set master branch to active branch
git merge new-feature # merge new-feature into master branch
git log --graph --oneline # show graphs and one-line per commit summary for non merging
git merge --abort # erase all changes and reverse to prior commit before attempted merge

# remote repos
git clone <URL>
git pull # fetch remote updates from repo
git push # push commits to remote repo
git remote -v  # gives URLs for name of remote repo in current working dir
git remote show origin # show detailed info on <origin> repo
git branch -r # show branches in remote repo

# to modify remote repo, first pull changes from repo, then merge with local branch,
# the push back to origin

```

Branch - a pointer to a particular commit - independent line of development.  Default branch git creates for new repo is called the master. Master is known good state.  

Merge - combining branched data and history together

Two algorithms for merging:
-- fast-forward    - all commits in checked out branch are in the merged product
-- three-way merge - master may have changed since branching new-feature branch
                     so merging requires 3-way merge forming a NEW commit

Merge conflicts resolution - run git status if a merge conflict ensues and usually
tells you what to do to resolve.













