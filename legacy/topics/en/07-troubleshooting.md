# Troubleshooting
## Undoing Commits (`git revert`, `git reset`, `git checkout`)
### **`git revert`**
Used to **create a new commit that undoes the changes of a specific commit, preserving history.**
```bash
git revert <commit-hash>
```
This creates a new commit that undoes the changes of the specified commit.

This is what your log looks like, after `revert`: 
```bash 
loren@ MINGW64 /c/Projects/portfolio/git_study (dev)
$ git revert 0d3bd1def0f408e07b1249d7c599759b46380640
hint: Waiting for your editor to close the file...
[No write since last change]

Press ENTER or type command to continue
[No write since last change]

Press ENTER or type command to continue
[dev 68feb15] Revert "Commit para reverter"
 1 file changed, 1 insertion(+), 3 deletions(-)

loren@ MINGW64 /c/Projects/portfolio/git_study (dev)
$ git log
commit 68feb159e81c636e290febc9bbe0d94ac8a15ccb (HEAD -> dev)
Author: Lorenzo Uriel <lorenzo.uriel@.com.br>
Date:   Thu Jul 25 22:05:30 2024 -0300

    Revert "Commit para reverter"

    This reverts commit 0d3bd1def0f408e07b1249d7c599759b46380640.

commit 0d3bd1def0f408e07b1249d7c599759b46380640
Author: Lorenzo Uriel <lorenzo.uriel@.com.br>
Date:   Thu Jul 25 22:05:02 2024 -0300

    Commit para reverter
```

I made an initial `commit` with the message `Commit to revert`, then I got the commit hash and did a `git revert 0d3bd1def0f408e07b1249d7c599759b46380640` with the message `Revert "Commit to revert"`.

### **`git reset`**
Used to **reset the state of the repository to a previous commit.** The `reset` command can change history.

Main methods of `git reset`:
- `--soft`: Keeps files and indexing as they are, only resets the HEAD pointer
```bash
git reset --soft <commit-hash>
```

- `--mixed`: Keeps files in the working directory, but undoes index changes.
```bash
git reset --mixed <commit-hash>
```

- `--hard`: Resets the HEAD pointer, index, and working directory.
``bash
git reset --hard <commit-hash>
```

### **`git checkout`**
Used to **change branches or restore files in the working directory.** `Checkout` does not affect history. ```bash
git checkout <branch-name>
git checkout <commit-hash> -- <file-path>
```

## Common Conflict Resolution
### **Merge Conflicts**
When a merge conflict occurs, Git marks the conflicting files so you can resolve them manually.

**Example:**
```bash
git merge <branch-name>
```
Resolve conflicts by editing the conflicting files. Example message:
![merge](/ebook-pt//topics/imgs/07/merge_head.jpg)

```bash
loren@ MINGW64 /c/Projects/portfolio/git_study (main)
$ git merge dev
Auto-merging README.md
CONFLICT (/topics): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

- Mark conflicts as resolved:
```bash
git add <file-path>
```

- Complete the merge:
```bash
git commit -m "Fixed bugs, ready to go"
```

### **Rebase Conflicts**
During rebasing, conflicts are resolved in a similar way to merge conflicts.

**Example:**
```bash
git rebase <branch-name>
```

- Resolve conflicts by editing the conflicting files.

- Continue the rebase:
```bash
git rebase --continue
```

- To abort the rebase:
```bash
git rebase --abort
```

## Recovering Lost Commits
### **`git reflog`**
Keeps a record of all the **HEADs** that have been changed in the local repository.

It is often used for lost commits.

**Example:**
```bash
git reflog
```

- Identify the commit you want to recover and use `git checkout` or `git reset` to restore it.

Example of return in the terminal: 
```bash 
$ git reflog
76e8ecf (HEAD -> main) HEAD@{0}: commit (merge): Erros ok
3fd367d HEAD@{1}: commit: Vou fazer um merge
7ce5614 (origin/main) HEAD@{2}: checkout: moving from dev to main
1dbfda0 (dev) HEAD@{3}: checkout: moving from dev to dev
1dbfda0 (dev) HEAD@{4}: reset: moving to 1dbfda0a8363529fdbb0abb2023f7ee8f5d43691        
1dbfda0 (dev) HEAD@{5}: reset: moving to 1dbfda0a8363529fdbb0abb2023f7ee8f5d43691        
1dbfda0 (dev) HEAD@{6}: reset: moving to 1dbfda0a8363529fdbb0abb2023f7ee8f5d43691        
1dbfda0 (dev) HEAD@{7}: commit: Commit para dar um reset
68feb15 HEAD@{8}: revert: Revert "Commit para reverter"
0d3bd1d HEAD@{9}: commit: Commit para reverter
7ce5614 (origin/main) HEAD@{10}: rebase (finish): returning to refs/heads/dev
7ce5614 (origin/main) HEAD@{11}: rebase (start): checkout HEAD
7ce5614 (origin/main) HEAD@{12}: rebase (finish): returning to refs/heads/dev
7ce5614 (origin/main) HEAD@{13}: rebase (start): checkout HEAD
7ce5614 (origin/main) HEAD@{14}: rebase (finish): returning to refs/heads/dev
7ce5614 (origin/main) HEAD@{15}: rebase (start): checkout HEAD
7ce5614 (origin/main) HEAD@{16}: rebase (finish): returning to refs/heads/dev
7ce5614 (origin/main) HEAD@{17}: rebase (start): checkout HEAD
7ce5614 (origin/main) HEAD@{18}: rebase (finish): returning to refs/heads/dev
7ce5614 (origin/main) HEAD@{19}: rebase (start): checkout main
39f9d27 HEAD@{20}: checkout: moving from main to dev
7ce5614 (origin/main) HEAD@{21}: rebase (finish): returning to refs/heads/main
7ce5614 (origin/main) HEAD@{22}: rebase (start): checkout HEAD
7ce5614 (origin/main) HEAD@{23}: commit (merge): Commit 04
39f9d27 HEAD@{24}: rebase (finish): returning to refs/heads/main
39f9d27 HEAD@{25}: rebase (start): checkout HEAD
39f9d27 HEAD@{26}: checkout: moving from dev to main
39f9d27 HEAD@{27}: checkout: moving from main to dev
39f9d27 HEAD@{28}: checkout: moving from dev to main
39f9d27 HEAD@{29}: rebase (finish): returning to refs/heads/dev
39f9d27 HEAD@{30}: rebase (start): checkout main
52ec99f (origin/dev) HEAD@{31}: rebase (finish): returning to refs/heads/dev
52ec99f (origin/dev) HEAD@{32}: rebase (start): checkout HEAD
52ec99f (origin/dev) HEAD@{33}: checkout: moving from main to dev
```

### `git cherry-pick`
Used to **apply a specific commit from one branch to another.**

**Example:**
```bash
git cherry-pick <commit-hash>
```

## Troubleshooting Tips
### **Problem Diagnosis**
Use commands like `git status`, `git log`, and `git diff` to understand the current state of your repository and identify issues.
- `git status`: Provides an overview of the current state of your repository. It shows which files have been modified, which are ready to be committed, and which are untracked. This helps you quickly understand what has changed since your last commit.

- `git log`: Used to view the history of commits. This is useful for identifying changes made over time and understanding how the repository has evolved. You can add options like `--oneline` for a more concise view or `--graph` for a graphical representation of the commits.

- `git diff`: Compares changes between commits, between the repository and the working directory, or between different branches. It is useful for reviewing specific changes to files and understanding how the code was modified.

### **Ignore Files Locally**
If you need to ignore changes to files that are tracked, use
```bash
git update-index --assume-unchanged <file-path>
```

To undo:
```bash
git update-index --no-assume-unchanged <file-path>
```

### **Discard Local Changes**
To discard changes to modified files:
```bash
git checkout -- <file-path>
```

To discard all local changes:
```bash
git reset --hard
```

### **Troubleshoot Push/Pull Issues**
If you encounter problems when pushing or pulling, such as push rejections, first fetch to synchronize your repository:
```bash
git fetch
```
- Resolve any conflicts, then try again
---