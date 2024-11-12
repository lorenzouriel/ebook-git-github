# Git Restore and Git Switch

Starting with Git version 2.23, two new commands, `git restore` and `git switch`, were introduced to simplify workflows for restoring files and switching branches. These commands were designed to replace specific uses of the older `git checkout` command, which handled multiple functions and could sometimes be confusing.

### 1. Git Restore
The `git restore` command focuses on restoring files in your working directory. It provides a more intuitive way to discard changes, allowing you to reset files to their state in either the index (staging area) or a particular commit.

**Basic Syntax:**
```bash
git restore <options> <file>
```

**Common Options:**
- `--source <commit-hash>`: Restore files to the state they were in a specific commit.
- `--staged`: Restore files in the staging area (the index).
- `--worktree`: Restore files only in the working directory (default).

**Examples:**

- Restore a file in the working directory to match the last commit:
```bash
git restore <file>
```

- Unstage a file (remove it from staging without deleting changes):
```bash
git restore --staged <file>
```

- Restore a file to match a previous commit:
```bash
git restore --source <commit-hash> <file>
```

## 2. Git Switch
The `git switch` command simplifies the process of changing branches or creating new ones. It provides a more intuitive and focused way to manage branches compared to git checkout.

**Basic Syntax:**
```bash
git switch <options> <branch>
```

**Common Options:**
- `-c <branch>`: Creates a new branch and switches to it.
- `-C <branch>`: Creates a new branch or resets the branch if it already exists.
- `--detach`: Switches to a specific commit in "detached HEAD" state (not on any branch).
- `--discard-changes`: Discards any uncommitted changes when switching branches.

**Examples:**

- Switch to an existing branch:
```bash
git switch feature/develop-database
```

- Create and switch to a new branch:
```bash
git switch -c feature/develop-database
```

- Switch to a specific commit in a detached HEAD state:
```bash
git switch --detach <commit-hash>
```

### Key Differences from Git Checkout
- `git restore` is for modifying files in the working directory or index.
- `git switch` is for changing branches.
- `git checkout` still exists and can be used, but `git restore` and `git switch` offer more clarity and are better for specific use cases.



