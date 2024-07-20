# Git and GitHub Cheat Sheet

## Table of Contents
1. [Git Basics](#git-basics)
2. [Branching and Merging](#branching-and-merging)
3. [Remote Repositories](#remote-repositories)
4. [Stashing and Cleaning](#stashing-and-cleaning)
5. [Rewriting History](#rewriting-history)
6. [GitHub Features](#github-features)
7. [Collaboration](#collaboration)
8. [Advanced Tips](#advanced-tips)

---

## Git Basics

### Configuring Git
```sh
# Set your name and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Check configuration
git config --list
```

### Initialization and Cloning
```sh
# Initialize a new Git repository
git init

# Clone an existing repository
git clone https://github.com/user/repo.git
```

### Working with Commits
```sh
# Check status of working directory
git status

# Stage files for commit
git add <file>
git add .  # Stage all changes

# Commit staged files
git commit -m "Commit message"

# View commit history
git log
git log --oneline  # Compact view
```

## Branching and Merging

### Branch Management
```sh
# List branches
git branch

# Create a new branch
git branch <branch-name>

# Switch to a branch
git checkout <branch-name>

# Create and switch to a new branch
git checkout -b <branch-name>

# Delete a branch
git branch -d <branch-name>
git branch -D <branch-name>  # Force delete
```

### Merging
```sh
# Merge a branch into the current branch
git merge <branch-name>

# Abort a merge
git merge --abort
```

### Resolving Conflicts
```sh
# After resolving conflicts, stage the changes
git add <file>

# Continue with the merge
git commit
```

### Rebasing
```sh
# Rebase current branch onto another branch
git rebase <branch-name>

# Continue a rebase after resolving conflicts
git rebase --continue

# Abort a rebase
git rebase --abort
```

## Remote Repositories

### Managing Remotes
```sh
# Add a remote repository
git remote add origin https://github.com/user/repo.git

# List remote repositories
git remote -v

# Remove a remote repository
git remote remove <name>
```

### Pushing and Pulling
```sh
# Push changes to remote repository
git push origin <branch-name>

# Pull changes from remote repository
git pull origin <branch-name>

# Fetch changes from remote without merging
git fetch origin
```

## Stashing and Cleaning

### Stashing Changes
```sh
# Stash changes
git stash

# List stashes
git stash list

# Apply the latest stash
git stash apply

# Apply and drop the latest stash
git stash pop

# Drop a specific stash
git stash drop stash@{0}
```

### Cleaning
```sh
# Show what would be deleted
git clean -n

# Remove untracked files and directories
git clean -fd
```

## Rewriting History

### Amending Commits
```sh
# Amend the last commit
git commit --amend

# Amend with a new message
git commit --amend -m "New commit message"
```

### Reverting Commits
```sh
# Revert a commit
git revert <commit-hash>
```

### Resetting Commits
```sh
# Soft reset (keep changes in working directory)
git reset --soft <commit-hash>

# Mixed reset (default, keep changes in working directory but unstage them)
git reset <commit-hash>

# Hard reset (discard changes in working directory)
git reset --hard <commit-hash>
```

## GitHub Features

### Issues and Pull Requests
```sh
# Open a new issue
# On GitHub website, go to the Issues tab and click "New issue"

# Create a pull request
# On GitHub website, go to the Pull Requests tab and click "New pull request"
```

### GitHub Actions
```yaml
# Example GitHub Actions workflow file (.github/workflows/ci.yml)
name: CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.8'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Run tests
      run: |
        pytest
```

### GitHub Pages
```sh
# Deploy static site to GitHub Pages
# On GitHub website, go to Settings -> Pages and select the source branch
```

## Collaboration

### Forking and Pull Requests
```sh
# Fork a repository
# On GitHub website, click "Fork" button on the repository page

# Clone your fork
git clone https://github.com/your-username/repo.git

# Create a branch for your changes
git checkout -b feature-branch

# Push changes to your fork
git push origin feature-branch

# Create a pull request
# On GitHub website, go to your fork and click "Compare & pull request"
```

### Code Reviews
```sh
# Request a review
# On GitHub website, open the pull request and select reviewers
```

## Advanced Tips

### Aliases
```sh
# Create an alias for a Git command
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```

### .gitignore
```sh
# Example .gitignore file
*.log
*.tmp
*.swp
.DS_Store
node_modules/
dist/
```

### Submodules
```sh
# Add a submodule
git submodule add https://github.com/user/repo.git path/to/submodule

# Initialize and update submodules
git submodule update --init --recursive

# Remove a submodule
git submodule deinit -f path/to/submodule
rm -rf .git/modules/path/to/submodule
git rm -f path/to/submodule
```

### Git Hooks
```sh
# Example pre-commit hook (.git/hooks/pre-commit)
#!/bin/sh
# Check for trailing whitespace
if git grep -q " $" .; then
  echo "Error: Trailing whitespace found"
  exit 1
fi
```

### Reflog
```sh
# View reflog (history of all actions)
git reflog

# Restore a commit from reflog
git reset --hard <reflog-hash>
```
