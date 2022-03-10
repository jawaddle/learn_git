# PluralSight Git learning pathway course notes

## PluralSight GitHub course by Gill Cleeren

### Known markdown files on github

- README.md can be stored in root, .github or docs folder
- LICENSE, CONTRIBUTING, CONTRIBUTORS, CHANGELOG, SUPPORT, CODE_OF_CONDUCT, CODEOWNERS
- codeowners file must contain @accountname of github accounts of owners

### Repository features

- Topics
- Projects
- Issues
- Pull Requests
- Insights
- Settings

### Branching Strategies

- Centralized workflows
-- one central branch (main) to which all commits merge
- GitFlow workflow
-- main with hotfix branches
-- development with new feature and issue branches
- Forking workflow
-- open source option
-- contributors fork / copy repo, make changes and ask owner for pull request to merge their changes
- GitHub workflow
-- lightweight flow
-- favored by GitHub
-- branches for bugs, features, ...
-- revolves around pull requests

### PR templates

- pull_request_template.md in root folder

### issue

- issue labels that are built in
-- bug
-- duplicate 
-- enhancement
-- help wanted
-- question
-- wontfix
-- good first issue
-- invalid
-- documentation
- Can add issue templates 
-- automatically placed in .github/ISSUE_TEMPLATE

### milestone

- track progress to a certain point
- can be a group of issues
- usually include due date, progress, and list of open issues and pull requests and prioritess

### tag

- point to a certain point (snapshot) in repo history
- lightweight tag is just a pointer to a certain commit
- annotated tag is more comprehensive with meta data
-- git tag  # lists the tags that exist
-- git tag stable main # tags main branch with 'stable'
-- git log --oneline --graph --decorate --all
--git tag -a v0.1 -m "0.1 Release" fb08c # set annotated tag to specific commit fb08c
--git push --tags # need to push tags up to remote

### release

- based on tags but allow writing release notes in markdown format and link to binary files (exe)

### GitHub Actions

- automate different tasks
- event driven
- live inside the repo
- placed in .github/workflows directory
-- use YAML syntax
- part of github, not git
- many pre-existing templates for common workflows
- workflows made of one or more jobs that are triggered by events
- each job can have one or more steps that execute actions
- a 'Runner' is a server that coordinates and runs all these executable actions
- Runner server can be on github or on premise

### GitHub Wiki

- Markdown based documentation for the project
- Can be referenced by the README.md
- Can clone and work locally and push changes back up to remote

### GitHub Gists

- can share small story or code snippets (say reference gist from blog-post as script src= ...  tag
- still based on repo
- public or secret (although latter is not private, if someone has url, they can access, but just not searchable)
- downloadable
- create at gist.github.com
- can clone and work from local repo and push up changes as commit

### GitHub Projects

- project management - columnar - templatable - semi-automated 

### GitHub Pages

- static web site (no server side code)
- repo based
- online or offline editing
- link available and hosted on GitHub

## PluralSight git course by Aaron Stewart

```bash
git rm --cached filename # untracks but does not delete file in repo
git rm filename          # untracks and deletes file from repo
git reset --soft         # moves commit back to staging area
git reset --mixed        # moves commit back to working directory
git reset --hard         # deletes commit
```

## PluralSight How Git Works Paolo Perrotta

```bash
git cat-file -p <hash>   # prints contents of given hash
git count-objects        # counts number of objects in current git repo
git branch               # lists all branches and stars branch that is active
                         # and in the refs/head directory???
git branch <newbranch>   # creates new branch called newbranch
git switch <branchname>  # switch working directory to branch called branchname
git checkout <brname>    # switch to branchname
git checkout <hash>      # switch working directory to commit given by hash

```

- blobs = file contents
- trees = points to other directories/trees and blobs
- commits = pointers to tree
- annotated tags = git object that points to a commit
- branch just a pointer to a commit
- HEAD file in .git directory is just pointer to active commit branch
- if merge conflict, must change manually, then restage modified file before commit
- commits track history
- a detached HEAD does not point to a branch
- fast forward merge is just taking a recently merged branch and bringing in main

```bash
git switch ideas
git merge main
```

- if you detach HEAD from an active branch and make changes, then switch back to main branch, the new commits on the active branch will be garbage collected soon
- before GC, can just branch back to commits and list as branch to preserve commits
- REBASE: merges preserve history but rebase discards history in favor of a clean timeline with discarded merges
- tags are like branch names that cannot move
- .git/config contains all details needed to contact remote repo being tracked
- .git/refs/remotes hodls all remote repo branches
- never rebase shared commits
- forking clones remote repo but assigns remote to user forking the repo, not the original owners repo
- after fork made, the forker can make pull request to original owner to incorporate changes
- original remote from which repo was forked often dubbed 'upstream' rather than the forked version which is origin in the forkers github acct

```bash
git tag release1 -a -m "message" # current commit labeled with release1 annoated tag
git tag                          # lists all tags in repo
git checkout release1            # set working dir to release1 tagged commit
git cat-file -t <hash>           # show type of object pointed to by hash
git branch --all                 # lists all branches in repo
git show-ref main <hash>         # shows refs associated with <hash>
git show-ref <branchname>        # shows refs associated with <branchname>
git push -f    # Use with care: forces overwrite of remote with local

# preferred over git push -f
git fetch
git merge

# or
git pull # combines git fetch and git merge
```

 > Naming. Torvalds sarcastically quipped about the name git (which means "unpleasant person" in British English slang): "I'm an egotistical bastard, and I name all my projects after myself. First 'Linux', now 'git'."

## PluralSight Git: the big picture Paolo Perrotta

- largely a view of git and github from 37000 feet
- weakness of git: does not work well with large binary files

## GitHub Pull Requests from Start to Finish By Lisa Walkosz-Migliacion

- gitlab calls them merge-requests, not pull-requests

## Working with Git Branches By Craig Golightly

### Branching and Merging

```bash
git checkout -b quickfix    # Create and checkout new branch called quickfix
git switch -c quickfix      # Identical to previous checkout command with switch
git branch -m <oldbranchname> <newbranchname>  # rename a branch
git branch -m hotfix        # renames current branch as hotfix
git branch-d <branchname>   # deletes specified branch
                            # error msg if uncommitted work
git branch -D <branchname>  # force delete even if uncommitted work

# merge basics
git switch <target-branch>  # set target branch as working
git merge <source-branch>   # attempt to merge target onto source
                            # complete in the case of fast-forward merges

# previewing a desired merge 
git diff <branch-1> <branch-2>   # shows differences between tips (last commit) of branches
git diff <branch-1>...<branch-2> # diffs since branch-2 split from branch-1, eg. history
git diff <branch-1> <branch-2> <filename> # differences only in filename
git diff          # shows only changes between commit and unstaged file version
git diff --cached # shows only changes between already staged and committed
git diff HEAD     # shows all changes between commit and current
git diff -w       # ignores whitespace differences
git merge --abort # stop merge and restore directory to state prior to merge attempt
```

- dirty branch:  changes made to branch but not yet committed
- if you try to switch branches from a dirty branch to some other branch, will get a warning that must first commit changes before switching branches
- most editors will dynamically show changed context on branch switching if open
- cannot delete current working branch, must switch to another branch first
- target of merge is the branch you want to merge into (modify)
- source of merge is the branch that has the changes to modify the target
- understanding diff output
-- two files (derived from branch-1 and branch-2) labeled a and b respectively
-- index gives "hash of a...hash of b" # can reveal with git show hash
-- file markers: --- for a, +++ for b, or /dev/null for new or deleted file
-- chunk header: @@ -3,6 +3,7 @@ 
--- 6 lines of a-file starting on line 3, and 7 lines of b-file starting on line 3
--- following lines denoted with - for a, + for b, and no indicator for lines that do not differ
- merge conflict: something has changed in both branches, must fix manually, stage the modified file(s) and commit the new merge commit
- merge commit will have 2 parent commits
-- <<<< TARGET_BRANCH
-- ======= separator between file content
-- >>>> SOURCE_BRANCH
- must remove file markers and leave desired content before stage and commit
- if merge is still pending and incomplete MERGING is added to command prompt in bash. Go ahead and finish!

### Forking, Pull Requests

```bash
git remote add <name> <remote-url> # add new remote named <name> at specified url
git remote -v   # list remotes and urls
git fetch  # two step remote syncy
git merge
git pull   # combines git fetch and git merge in single command
git push   # conflicts with remote must be resolved before pushing
git remote update # refresh remote so that git status reflects local vs. remote
                  # differences
git ls-remote     # lists remote branches
git push -u origin <new-branch>  # push new-branch to remote site origin
git fetch origin <new-branch>    # pull down new-branch to local repo
git branch -a                    # lists all local and remote branches
git checkout --track origin <new-branch>  # local now tracks remote new branch

```

- fork, clone, git status, git remote -v 
- default name for remote is origin
- can set up alternative name 
- can push a branch to remote without merging say prior to working on another remote machine
- pull request workflow
-- push branch to remote
-- open pull request
-- Admin adds reviewers
-- Admin suggests changes
-- Make fixes in local branch
-- push to remote (do not rebase after pushing to remote)
-- can now delete feature branch once pull request complete
- consider using feature flags for new code base in build to make rollback easy by setting feature flag to false
- do not leave commented code blocks in commits
- be aware of line ending differences and whitespace

### .gitignore

- in addition to .gitignore, can make entries in .git/info/exclude to ignore files specific to this project

### Advanced merging methods

```bash
# squash several commits into a single commit
# say 3 commits in ticket1 branch and want to squash into 1 before merge into main
git log --oneline # reveals all commits
git merge-base ticket1 main # will show the sha1 hash of first commit in main
git rebase -i hash-of-main-from-previous command
# git will show commit message
# change second and third commits from 'pick' to 'squash' and make any adjustments to commit message - it will inform of changes to HEAD
git log # should reveal only the single squashed commit on ticket1

# Rebase from main into ticket2 branch
git switch ticket2
git rebase main
git ref-log  # provides history of above

# Upstream rebase if you pulled, did some work
# then the upstream team squashed down (rebased)
# several commits on upstream branch.  Now your commits
# will be off
# To restore do a git pull --rebase
git pull --rebase # from forked work will identify
                  # commit in squashed work and reset
                  # to a decent point with mimimal conflict

# Cherry picking
git log --oneline # find commits you want to cherry-pick
git log branchname --oneline # examine non-current branches
git checkout branchname      # checkout branch with commit to CP
git cherry-pick <commit-sha>   # pull commit into current branch
git cherry-pick  # copy specific commits to another branch

```

- do not use rebase on a public or shared branch
- more appropriate - use rebase to clean up local branch before sharing a branch
- pulling changes from a branch into your branch without performing a merge
- squash several commits into a single commit
- Cherry-pick
-- say pull down commit for a bug fix to patch multiple versions of software that are in distinct branches
-- capture commits from an inactive branch
-- cherry-pick creates a duplicate commit in each branch

