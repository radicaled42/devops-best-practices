# Git Commands

## Git Config

`git config`

Example: `git config --global user.name "Your Name"`

`git config --global`

Example: `git config --global user.mail "your.mail@example.com"`

## Creating a Repository

`git init`: Initialize a git repository

Example: `git init new-project`

`git clone`: Used to download existing code from a remote repository

Example: `git clone https://github.com/user/repository.git`

`git remote`

Example: `git remote add origin https://github.com/user/repository.git`

## Making Changes

`git add`: Add files to the staging area

Example: `git add .`

`git status`: Used to check the state of the staging area, as well as the working directory

Example: `git status`

`git commit`: Used to commit files (locally) on the repository

Example: `git commit -m "initial commit"`

`git log`: Used to view the entire commit history

Example: `git log --oneline`

`git diff`: Display the differences between files in two commits or between a commit and your current repository

Example: `git diff HEAD~1 HEAD`

## Undoing Changes

`git reset`: Undo the changes to the local files and restore the last commit

Example: `git reset HEAD~1`

`git revert`

Example: `git revert abc123`

`git clean`

Example: `git clean -fd`

## Repote Repositories

`git fetch`

Example: `git fetch origin`

`git pull`: Used to pull down all the updates from a remote repository

Example: `git pull origin main`

`git push`: Used to save all commits to the remote repository

Example: `git push origin feature-branch`

`git remote`

Example: `git remote -v`

## Branching and Merging

`git branch`: Used to list all the local branches on the machine

`git branch <branch-name>`: Used to create a new branch locally

Example: `git branch new-feature`

`git branch -d <branch-name>`: Used to delete a branch

Example: `git branch -d feature`

`git branch -m <branch-name>`: Used to rename the current branch

Example: `git branch -m new-feature`

`git checkout`: Used to switch between branches

Example: `git checkout -b bugfix-123`

`git merge`: Merges the provided branches on the machine

Example: `git merge feature-branch`

`git rebase`

Example: `git rebase main`

## Git Flow

`git flow init`

Example: `git flow init -d`

`git flow feature`

Example: `git flow feature start new-feature`

`git flow release`

Example: `git flow release start v1.0.0`

`git flow hotfix`

Example: `git flow hotfix start bugfix-123`

`git flow support`

Example: `git flow support start v1.5`
