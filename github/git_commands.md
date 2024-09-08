# **Git Commands Cheat Sheet**

Git is a powerful version control system used to track changes in your code, collaborate with others, and manage your project's history. Below is a collection of common Git commands, organized by category, along with examples to help you get started.

---

## **Git Config**

`git config`: Configure user information for all local repositories or a specific one.

- **Example:** `git config --global user.name "Your Name"`

`git config --global`: Set global configurations like username and email.

- **Example:** `git config --global user.email "your.email@example.com"`

---

## **Creating a Repository**

`git init`: Initialize a new Git repository.

- **Example:** `git init new-project`

`git clone`: Clone an existing repository from a remote source.

- **Example:** `git clone https://github.com/user/repository.git`

`git remote`: Manage set of tracked repositories.

- **Example:** `git remote add origin https://github.com/user/repository.git`

---

## **Making Changes**

`git add`: Add files to the staging area, preparing them for a commit.

- **Example:** `git add .`

`git status`: Show the status of the working directory and staging area.

- **Example:** `git status`

`git commit`: Record changes to the repository with a message.

- **Example:** `git commit -m "initial commit"`

`git log`: Show the commit history for the repository.

- **Example:** `git log --oneline`

`git diff`: Show changes between commits, branches, or working directories.

- **Example:** `git diff HEAD~1 HEAD`

---

## **Undoing Changes**

`git reset`: Undo changes by moving the HEAD to a previous commit.

- **Example:** `git reset HEAD~1`

`git revert`: Create a new commit that undoes the changes of a previous commit.

- **Example:** `git revert abc123`

`git clean`: Remove untracked files from the working directory.

- **Example:** `git clean -fd`

---

## **Remote Repositories**

`git fetch`: Download objects and refs from another repository.

- **Example:** `git fetch origin`

`git pull`: Fetch and integrate changes from the remote repository to the local branch.

- **Example:** `git pull origin main`

`git push`: Upload local commits to the remote repository.

- **Example:** `git push origin feature-branch`

`git remote -v`: List all remote connections along with their URLs.

- **Example:** `git remote -v`

---

## **Branching and Merging**

`git branch`: List, create, or delete branches.

- **Example (List branches):** `git branch`
- **Example (Create branch):** `git branch new-feature`
- **Example (Delete branch):** `git branch -d feature`
- **Example (Rename branch):** `git branch -m new-feature`

`git checkout`: Switch branches or restore working tree files.

- **Example (Switch branches):** `git checkout new-feature`
- **Example (Create and switch):** `git checkout -b bugfix-123`

`git merge`: Join two or more development histories together.

- **Example:** `git merge feature-branch`

`git rebase`: Reapply commits on top of another base tip.

- **Example:** `git rebase main`

---

## **Git Flow**

`git flow init`: Initialize a git-flow repository, setting up the required branches.

- **Example:** `git flow init -d`

`git flow feature`: Manage feature branches.

- **Example:** `git flow feature start new-feature`

`git flow release`: Manage release branches.

- **Example:** `git flow release start v1.0.0`

`git flow hotfix`: Manage hotfix branches.

- **Example:** `git flow hotfix start bugfix-123`

`git flow support`: Manage support branches.

- **Example:** `git flow support start v1.5`

---

This cheat sheet should help you get started with Git or refresh your knowledge of its commands. Happy coding!
