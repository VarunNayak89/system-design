# 🧰 Git Commands Cheat Sheet

This document summarizes essential **Git** commands for managing repositories, branches, remotes, and commits.

---

## 🔗 SHARE & UPDATE (Remote Operations)

### Add Remote
```bash
git remote add [alias] [url]
```
- Adds a Git URL as an alias.  
- Common alias name: `origin`  
- Example:
  ```bash
  git remote add origin https://github.com/user/repo.git
  ```

### List Remotes
```bash
git remote -v
```
- Lists remote GitHub connections.  
- If no remote is configured, it will not return anything.

### Remove Remote
```bash
git remote remove origin
```
- Removes the `origin` remote from your repository.

### Fetch from Remote
```bash
git fetch [alias]
```
- Downloads all branches from the given Git remote.

### Merge Remote Branch
```bash
git merge [alias]/[branch]
```
- Merges a remote branch into your current branch to bring it up to date.

### Push to Remote
```bash
git push [alias] [branch]
```
Example:
```bash
git push -u origin master
```
- Sends local branch commits to the remote repository branch.

### Pull from Remote
```bash
git pull [alias] [branch]
```
Example:
```bash
git pull origin master
```
- Pulls the latest changes from the specified remote and branch.  
- If not specified, it defaults to the origin’s main/master branch.

---

## 🌿 BRANCH & MERGE

### List Branches
```bash
git branch
```
- Lists all branches.  
- The `*` symbol indicates the currently active branch.

### Create a Branch
```bash
git branch [branch-name]
```
- Creates a new branch at the current commit.

### Switch Branch
```bash
git checkout [branch-name]
```
or
```bash
git switch [branch-name]
```
- Switches to another branch and checks it out into your working directory.

### Create and Switch
```bash
git checkout -b [branch-name]
```
- Creates a new branch **and** switches to it.

### Merge Branch
```bash
git merge [branch]
```
- Merges the specified branch’s history into the current one.

### View Commit History
```bash
git log
```
- Shows all commits in the current branch’s history.

---

## 📸 STAGE & SNAPSHOT

### Check Status
```bash
git status
```
- Shows modified and staged files.

### Stage Changes
```bash
git add .
```
- Stages all changes for the next commit.  
- You can also add specific files or folders:
  ```bash
  git add file.txt
  git add folder-name/*
  ```

### Unstage a File
```bash
git reset [file]
```
- Removes a file from the staging area but keeps changes in your working directory.

### Show Differences
```bash
git diff
```
- Shows changes that are **not staged**.

### Show Staged Differences
```bash
git diff --staged
```
- Shows what is **staged** but not yet committed.

### Commit Changes
```bash
git commit -m "[descriptive message]"
```
- Commits staged work as a new snapshot.  
- Always use a clear and descriptive message.

### Discard Local Changes
```bash
git restore .
```
- Discards uncommitted changes in your working directory.

---

## 🧩 CLONE REPOSITORY

### Clone Existing Repository
```bash
git clone [url]
```
- Creates a local copy of a remote repository.

---

## ⚙️ GENERAL GIT COMMANDS

### Initialize a Repository
```bash
git init
```
- Initializes a new Git repository in the current directory.

### Push with Upstream Tracking
```bash
git push --set-upstream origin [branch]
```
Example:
```bash
git push --set-upstream origin varun
```

### Set Upstream Branch
```bash
git branch --set-upstream-to=origin [branch]
```
Example:
```bash
git branch --set-upstream-to=origin varun
```

---

## 👤 CONFIGURE GIT USER

These settings identify you in commit history.

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

✅ **Tip:** Always run `git status` before pushing or committing to verify what’s staged, modified, or pending.
