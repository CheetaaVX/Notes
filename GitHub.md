## 1. Getting Started with Git

### `git init`

> Initializes a **new Git repository** in the current directory.  
> You’ll use this when starting a new project **locally**.

```bash
git init
```

Creates a `.git/` folder — this is where Git tracks all changes.

---

### ➤ `git clone <repo-url>`

> Downloads an existing Git repository (e.g., from GitHub) to your local system.

```bash
git clone https://github.com/username/repo-name.git
```

 This sets up a `.git/` folder and connects to the **remote repository** automatically.

---

##  2. Tracking Changes

### ➤ `git status`

> Shows the status of files — modified, staged, or untracked.

```bash
git status
```

Helpful to know what files are **ready to commit** and what still needs attention.

---

### ➤ `git add <filename>` or `git add .`

> Stages file(s) for commit.  
> You must add changes before you commit them.

```bash
git add index.html         # single file
git add .                  # all files
```

---

### ➤ `git commit -m "message"`

> Records the staged changes with a message.

```bash
git commit -m "Added user login page"
```

Each commit is like a **snapshot** of your project.

---

### ➤ `git log`

> Shows commit history.

```bash
git log
```

Great for tracking who made what change and when.

---

### ➤ `git diff`

> Shows the **line-by-line differences** between versions of files.

```bash
git diff index.html
```

 Useful to review changes before staging.

---

##  3. Working with Branches

### ➤ `git branch`

> Lists local branches.

```bash
git branch
```

---

### ➤ `git branch <branch-name>`

> Creates a **new branch**.

```bash
git branch feature-login
```

---

### ➤ `git checkout <branch-name>`

> Switches to a branch.

```bash
git checkout feature-login
```

---

### ➤ `git checkout -b <branch-name>`

> Creates and switches to a new branch.

```bash
git checkout -b feature-login
```

---

### ➤ `git merge <branch-name>`

> Merges the given branch into the current branch.

```bash
git merge feature-login
```

 Use this when your feature branch is complete and ready to be merged into `main`.

---

##  4. Pushing to and Pulling from GitHub

### ➤ `git remote -v`

> Shows the URLs of connected remotes like GitHub.

```bash
git remote -v
```

---

### ➤ `git push origin <branch>`

> Pushes commits to the remote branch on GitHub.

```bash
git push origin main
```

This updates the GitHub repo with your local commits.

---

### ➤ `git pull origin <branch>`

> Fetches and merges changes from GitHub.

```bash
git pull origin main
```

Helps keep your local project in sync with GitHub.

---

### ➤ `git fetch`

> Downloads changes from the remote, **but does not merge** them.

```bash
git fetch origin
```

---

## 5. Undo & Fix Mistakes

### ➤ `git restore <file>`

> Discards local changes in your working directory.

```bash
git restore index.html
```

---

### ➤ `git reset <file>`

> Unstages a file that was added accidentally.

```bash
git reset index.html
```

---

### ➤ `git reset --hard HEAD`

> Removes **all** changes (both staged and unstaged).

```bash
git reset --hard HEAD
```

**Dangerous**: You will lose changes permanently.

---

### ➤ `git revert <commit>`

> Creates a new commit that undoes a previous one.

```bash
git revert 7f5e3ab
```

 Safe alternative to `reset` if you’ve already pushed.

---

##  6. Temporary Saves with Stash

### ➤ `git stash`

> Temporarily saves uncommitted changes.

```bash
git stash
```

### ➤ `git stash pop`

> Applies the last stashed changes back to your working directory.

```bash
git stash pop
```

 Useful when switching branches and you’re not ready to commit.

---

##  7. Setup SSH for GitHub

### ➤ Generate SSH Key:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### ➤ Add key to SSH agent:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

### ➤ Add public key to GitHub:

Copy your key:

```bash
cat ~/.ssh/id_rsa.pub
```

Paste it to GitHub under **Settings > SSH and GPG Keys**.

---

##  8. Configuration (One Time Setup)

### ➤ Set your name and email:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### ➤ View current config:

```bash
git config --list
```

---

## Recommended Workflow Example

```bash
git clone <repo>
cd repo/
git checkout -b new-feature
# Make changes
git add .
git commit -m "Added new feature"
git push origin new-feature
# Create pull request on GitHub
```



