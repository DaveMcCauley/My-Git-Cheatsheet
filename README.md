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

## Tags

#### Renaming
Rename ```old``` tag to ```new```

```html
git tag new old
git tag -d old
git push origin :refs/tags/old
git push --tags
```
Finally, make sure that the other users remove the deleted tag. Please tell them (co-workers) to run the following command:
```html
git pull --prune --tags
```

Delete tag off remote

You just need to push an 'empty' reference to the remote tag name:

git push origin :tagname
Or, more expressively, use the --delete option (or -d if your git version is older than 1.8.0):

git push --delete origin tagname
If you also need to delete the local tag, use:

git tag --delete tagname

## Files

#### Add an existing file to `.gitignore`

Let’s say you have already added/committed some files to your git repository and you then add them to your .gitignore; these files will still be present in your repository index. This article we will see how to get rid of them.

Step 1: Commit all your changes
Before proceeding, make sure all your changes are committed, including your .gitignore file.

Step 2: Remove everything from the repository
To clear your repo, use:

`git rm -r --cached . ` 

`rm` is the remove command
`-r` will allow recursive removal
`–cached` will only remove files from the index. Your files will still be there.
The ` . ` indicates that all files will be untracked. 

You can untrack a specific file with `git rm --cached foo.txt` (thanks @amadeann).

The rm command can be unforgiving. If you wish to try what it does beforehand, add the `-n` or `--dry-run` flag to test things out.

Step 3: Re add everything
`git add .`

Step 4: Commit
`git commit -m ".gitignore fix"`

Push the changes to your remote to see the changes effective there as well.
