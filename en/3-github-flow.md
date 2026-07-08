# Module 3: Collaborative Development with GitHub 🤝

GitHub is a cloud platform that hosts Git repositories. It acts as a central hub where developers store code and collaborate using a structured workflow.

---

## 3.1 Working with Remotes

A **remote repository** is a version of your project hosted on a server (like GitHub).

### 1. `git clone`
Downloads an existing repository from GitHub to your computer.
```bash
git clone https://github.com/username/repository.git
```

### 2. `git remote add`
Links your local repository to a remote repository on GitHub (usually named `origin`).
```bash
git remote add origin https://github.com/username/repository.git
```

### 3. `git push`
Uploads local commits to GitHub.
```bash
git push origin main
```

### 4. `git pull`
Downloads the latest changes from GitHub and integrates them into your current local branch.
```bash
git pull origin main
```

---

## 3.2 Branching & Merging

Branches allow you to develop new features or fix bugs in an isolated environment without affecting the stable `main` codebase.

```
       (Feature Branch)      [*] ---> [*]
                            /            \
`main` branch: ------------[*]------------[*] (Merged)
```

### 1. `git branch`
Lists the branches in your project.
```bash
git branch
```

### 2. Creating a Branch
Creates a new branch named after your feature.
```bash
git branch feature-login
```

### 3. Switching Branches (`git checkout` or `git switch`)
Moves you to the specified branch.
```bash
git checkout feature-login
# Or:
git switch feature-login
```
*   *Shortcut (Create and Switch):* `git checkout -b feature-login`

### 4. `git merge`
Combines changes from another branch into your current active branch.
To merge `feature-login` into `main`:
```bash
git checkout main
git merge feature-login
```

---

## 3.3 Resolving Conflicts

A merge conflict happens when Git cannot automatically merge changes (for example, if two people edited the exact same line of a file differently).

When a conflict occurs, Git pauses the merge and marks the conflict in the file:
```
<<<<<<< HEAD
Our changes here on the main branch
=======
Their changes here on the feature branch
>>>>>>> feature-login
```

### How to resolve it:
1.  Open the file in a text editor.
2.  Choose which changes to keep and delete the Git markers (`<<<<<<<`, `=======`, `>>>>>>>`).
3.  Save the file.
4.  Add the resolved file to staging: `git add <filename>`
5.  Commit the merge: `git commit -m "merge: Resolve conflicts"`

---

## 3.4 The GitHub Flow

The standard workflow for contributing code in a professional environment is:

1.  **Fork:** Copy someone else's repository to your own GitHub account.
2.  **Clone:** Download your fork locally.
3.  **Branch:** Create a branch for your feature.
4.  **Commit & Push:** Make your changes and push the branch to your fork.
5.  **Pull Request (PR):** Open a PR on GitHub to propose merging your branch into the original main repository.
6.  **Code Review:** Discuss changes, make edits, and get approval.
7.  **Merge:** The project maintainers merge your PR!

---

[⬅️ Back to Main Index](../README.md)
