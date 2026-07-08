# Module 2: Version Control with Git 🌿

Git is the industry-standard tool for tracking changes in code. It allows multiple developers to work on the same project without overwriting each other's work and keeps a history of every change.

---

## 2.1 What is Git & Local Workflow

Think of Git as a local history machine. In Git, files go through three main areas before being permanently saved:

1.  **Working Directory:** The folder on your computer where you write code.
2.  **Staging Area:** A middle-ground index where you select which changes are ready to be saved.
3.  **Local Repository (.git folder):** The database where Git permanently stores your project's snapshots.

```
Working Directory   --->   Staging Area   --->   Local Repository
   (Editing)                (git add)              (git commit)
```

---

## 2.2 Tracking Changes

To start tracking a project, you must initialize Git.

### 1. `git init`
Run this once inside your project's root folder to start tracking.
```bash
git init
```

### 2. `git status`
Shows the current state of your project: which files have changed, which are in the Staging Area, and which are untracked.
```bash
git status
```

### 3. `git add`
Moves changes from the Working Directory to the Staging Area.
```bash
git add script.py      # Stage a specific file
git add .              # Stage all changes in the current folder
```

### 4. `git commit`
Saves a snapshot of the Staging Area to the Local Repository. Every commit requires a descriptive message.
```bash
git commit -m "feat: Add user login functionality"
```

---

## 2.3 History & Inspecting Commits

Once you have made commits, you can view the timeline of your project.

### 1. `git log`
Shows the list of commits, their unique ID (hash), the author, date, and commit message.
```bash
git log
# Press 'q' to exit the log view
```
*   `git log --oneline`: A compact view showing one line per commit.

### 2. `git show`
Shows the exact changes (diff) introduced in a specific commit.
```bash
git show <commit-hash>
```

---

## 2.4 Undoing Mistakes

Git is highly forgiving. If you make a mistake, you can undo it.

### 1. Discarding Unstaged Changes (`git restore`)
If you edited a file but want to reset it to how it looked in your last commit:
```bash
git restore index.html
```

### 2. Unstaging a File (`git restore --staged`)
If you accidentally ran `git add` and want to remove the file from Staging:
```bash
git restore --staged index.html
```

### 3. Moving to a Past Commit (`git checkout`)
Temporarily switch your working directory to view your project at a specific point in time.
```bash
git checkout <commit-hash>
# To go back to the present (main branch):
git checkout main
```

---

[⬅️ Back to Main Index](../README.md)
