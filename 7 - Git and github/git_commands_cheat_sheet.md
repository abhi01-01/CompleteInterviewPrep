
# 📌 Git Commands Cheat Sheet

## 🔹 Setup & Configuration
- `git config --global user.name "Your Name"` → Sets your global Git username.  
- `git config --global user.email "your@email.com"` → Sets your global Git email.  
- `git config --list` → Displays all Git configurations.  

---

## 🔹 Getting Started
- `git init` → Initializes a new Git repository in the current directory.  
- `git clone <repo_url>` → Clones a remote repository into a local directory.  

---

## 🔹 Basic Snapshotting
- `git status` → Shows the status of changes (staged, unstaged, untracked).  
- `git add <file>` → Stages a file for commit.  
- `git add .` → Stages all modified/untracked files in the current directory.  
- `git commit -m "message"` → Commits staged changes with a message.  
- `git commit -am "message"` → Adds & commits tracked files in one step.  

---

## 🔹 Branching & Merging
- `git branch` → Lists all local branches.  
- `git branch <name>` → Creates a new branch.  
- `git checkout <branch>` → Switches to a branch.  
- `git checkout -b <branch>` → Creates and switches to a new branch.  
- `git merge <branch>` → Merges a branch into the current branch.  
- `git branch -d <branch>` → Deletes a branch.  
- `git switch <branch>` → Alternative to checkout for switching branches.  
- `git switch -c <branch>` → Creates and switches to a new branch.  

---

## 🔹 Remote Repositories
- `git remote -v` → Lists all remote repositories.  
- `git remote add origin <url>` → Adds a remote repository.  
- `git remote remove <name>` → Removes a remote.  
- `git fetch` → Downloads objects and refs from a remote repo (without merging).  
- `git pull` → Fetches and merges changes from the remote repo into current branch.  
- `git push` → Pushes committed changes to remote repo.  
- `git push -u origin <branch>` → Pushes branch to remote and sets upstream tracking.  

---

## 🔹 Stashing & Cleaning
- `git stash` → Temporarily saves uncommitted changes.  
- `git stash pop` → Restores stashed changes and removes them from stash.  
- `git stash apply` → Restores stashed changes but keeps them in stash.  
- `git clean -f` → Removes untracked files from working directory.  

---

## 🔹 Viewing & Comparing
- `git log` → Shows commit history.  
- `git log --oneline` → Compact commit history.  
- `git diff` → Shows unstaged changes between working directory and index.  
- `git diff --staged` → Shows staged changes vs last commit.  
- `git show <commit_id>` → Shows details of a specific commit.  

---

## 🔹 Undoing Changes
- `git restore <file>` → Discards changes in working directory.  
- `git restore --staged <file>` → Unstages a file.  
- `git reset <file>` → Unstages file (older version of restore).  
- `git reset --hard <commit>` → Resets current branch to commit, discarding changes.  
- `git revert <commit>` → Creates a new commit that undoes changes from a previous commit.  

---

## 🔹 Tagging & Releases
- `git tag` → Lists all tags.  
- `git tag <name>` → Creates a new tag.  
- `git tag -a <name> -m "message"` → Creates an annotated tag.  
- `git push origin <tag>` → Pushes a tag to remote.  
- `git push --tags` → Pushes all local tags to remote.  

---

## 🔹 Collaboration & Workflow
- `git rebase <branch>` → Moves commits on top of another branch.  
- `git cherry-pick <commit>` → Applies a specific commit to current branch.  
- `git blame <file>` → Shows who last modified each line of a file.  
- `git shortlog` → Summarizes commit history by author.  

---

## 🔹 Advanced / Useful
- `git reflog` → Shows history of HEAD changes (safety net for lost commits).  
- `git bisect` → Finds commit that introduced a bug by binary search.  
- `git archive` → Creates a tar/zip of repository content.  
- `git submodule add <repo_url>` → Adds a submodule to a repo.  

---