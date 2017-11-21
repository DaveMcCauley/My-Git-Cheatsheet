# My-Git-Cheatsheet

## Remotes
#### Basics
```html
git remote -v  
git remote show <remote>  
git remote rename <old> <new>  
git remote remove <remote>

git remote prune  # remove unused brancehs
```
#### Remote Branches
```html
git branch --set-upstream-to=<remote>/<branch>     # set tracking
git checkout -b <new-branch> <remote>/<new-branch> # new branch

git fetch {--all, <branch>}   
git rebase <remote>/<branch>  # for each branch

git pull           # makes merge commit
git pull --rebase  # avoids merge, destroys any local changes

git push
git push -u <remote> <branch>
  
```

Rename a branch on a remote
```html
git branch -m <old-branch> <new-branch>       # rename the branch
git push origin :<old-branch>                 # delete the old branch
git push --set-upstream <remote> <new-branch> # creates and tracks remote

# each remote...
  git fetch origin         # fetches new branch
  git remote prune origin  # clears out the unused-
```

Delete a remote branch

```html
For example: git branch --delete origin fix/authentication
git push --delete <remote> <branch>.
```

## Branches
#### Basics
```html
git branch <new-branch>
git checkout -b <new-branch>                    # new branch, and switches to it.
git checkout -b <new-branch> <remote>/<branch>  # new branch, tracks remote

git checkout <branch>

git branch -m <new-name>             # renames current branch
git branch -m <old-name> <new-name>  # renames any branch

git branch -d <branch-to-delete>

git merge <branch-to-merge>          # allows fast forward
git merge <branch-to-merge> --no-ff  # forces merge commit
git branch --no-merged               # no merges allowed

git diff <branch> <branch>
```

Undo Inadvertant Fast Forward
```html
A-B-------master    A-B-C-D
   \    /
    C--D

git checkout master
git reset --hard <sha-B>
git checkout develop
git reset --hard <sha-D>  # if necessary
git checkout master
git merge develop --no-ff
```

Start a Branch at a Previous Commit
```html
git checkout <sha-commit>
git branch <new-branch>
```

## Commits
#### Basics
```html
git reset <las-good-sha>            # undo all commits, but perserves local changes
git reset --hard <last-good-sha>    # like it never happened
git reset --soft <origin>/<master>  # rollback to same commit as origin/master
                                      but keep changes and moves files to staging
                              
git checkout -- <file-name>         # discard changes to the last commited state

# git reset, git checkout can undo the undo from above.
```
Committed on the wrong branch (not pushed)
```html
git reset --soft HEAD~1
git checkout <desired-branch>
git commit 
```

Changes (not committed) on wrong branch
```html
git checkout -b <new-branch>    # keeps working changes
-or-
git checkout <exiting-branch>   # keeps working changes
```

