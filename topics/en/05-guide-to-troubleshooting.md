# A Guide to Troubleshooting
If something goes wrong, you need to know how to respond, Git isn’t just about the happy path:
- You work
- You make a commit
- Merge Branch
- Deploy Changes

We love the happy path, that's why is happy!

But more often than not, things don’t go as planned and we need to know how to react in that cases.

How do you recover lost changes? How do you revert mistakes?

This isn’t just about Git, it applies to every project.

That’s exactly what I’ll cover in this chapter.

## Undoing Commits (git revert, git reset, git checkout)
When working with Git, you may need to undo commits for some reasons, such as fixing errors, reverting unexpected changes, or cleaning up history. 

Git provides three main commands for undoing commits: `git revert`, `git reset` and `git checkout`. Each has a different behavior and should be used accordingly.

## git revert
`git revert` creates a new commit that undoes the changes introduced by a specific commit without modifying the repository history. 

This is useful when you want to keep the history clean and not remove commits.

### Usage:
```bash
git revert commit-hash
```

### Example:
1. Check the commit you want to revert:
```bash
git log --oneline 

# Return
PS C:\ebooks\git-github-ebook-test> git log --oneline 
56c9845 revert
3d87987 herge tag 'v1.0' into dev Showw show
d207431 (tag: v1.0, main) Merge branch 'release/v1.0'
28b146b Yes
0a91ea2 Updated commit message
ca382f6 (origin/main) filename3
db14708 new file
5a26f39 (tag: v1.0.0) first commit
PS C:\ebooks\git-github-ebook-test> 
```

2. Copy the hash and run `git revert`:
```bash
git revert 56c9845

# Return
PS C:\ebooks\git-github-ebook-test> git log --oneline 
4134ad2 (HEAD -> dev) Revert "revert"
56c9845 revert
3d87987 herge tag 'v1.0' into dev Showw show
d207431 (tag: v1.0, main) Merge branch 'release/v1.0'
28b146b Yes
0a91ea2 Updated commit message
ca382f6 (origin/main) filename3
db14708 new file
5a26f39 (tag: v1.0.0) first commit
PS C:\ebooks\git-github-ebook-test> 
```
- This creates a new commit that reverts the changes from commit `56c9845`.


## `git reset`

`git reset` moves the HEAD pointer to a previous commit, this is used for modifying commit history. It has three main modes:

### Modes of `git reset`:

- **Soft (`--soft`)**: Resets the HEAD to a previous commit but keeps the changes in the staging area, allowing you to modify or amend the commit.
- **Mixed (`--mixed`)** (default): Resets the HEAD to a previous commit and removes the changes from the staging area, but leaves the changes in the working directory.
- **Hard (`--hard`)**: (default): Resets the HEAD to a previous commit and removes the changes from the staging area, but leaves the changes in the working directory.

### `--soft` Example:
The `--soft` option undoes the last commit, but keeps the changes in the staging area, so you can easily modify the commit or change the commit message. This is useful if you want to redo a commit without losing the work you've done.
```bash
git reset --soft HEAD~1 
```
- In this example, `HEAD~1` moves the HEAD back by one commit, but the changes remain staged, so you can re-commit them after making adjustments.


### `--mixed` Example:
The `--mixed` option resets the HEAD to the specified commit, removes the changes from the staging area, but leaves them in the working directory. This is the default behavior of `git reset` if no mode is specified.
```bash
git reset --mixed HEAD~1
```
- This command undoes the last commit and unstages the changes, but the changes remain in your working directory, so you can still modify them.

### `--hard` Example:
The `--hard` option resets both the staging area and the working directory to match the specified commit. This means all changes are lost and cannot be recovered unless you have backups or use `git reflog`.
```bash
git reset --hard HEAD~1
```
- This will remove the last commit and all the changes associated with it, both in the staging area and the working directory.


## `git checkout`

`git checkout` can be used to undo changes in individual files or switch branches. We've talked about him only for branches since now.

It was also used for undoing commits, but now `git switch` and `git restore` are recommended for these tasks to provide a clearer, more specific functionality.

### Usage to restore specific files:
`git checkout` can be used to undo changes in individual files and restore them to the last committed state.
```bash
git checkout -- filename.txt
```
- This command will discard any uncommitted changes in the `filename.txt` file and restore it to its last committed state.

The `--` is used to tell Git that you're referring to a file (not a branch) and you want to discard changes in the working directory, restoring the file to the state of the last commit.
command will discard any uncommitted changes in the `filename.txt` file and restore it to its last committed state.

### `git restore` Example:
`git restore` is the recommended command for restoring files, and it's more intuitive than using `git checkout` for this purpose.
```bash
git restore filename.txt
```
- This command will discard any uncommitted changes in the `filename.txt` file and restore it to the version from the last commit, just like `git checkout -- filename.txt`.

## Recovering Lost Commits
If you accidentally lose a commit in Git, you can recover it using commands like git reflog and git fsck. These tools help you identify and restore commits that seem to have been lost.

### Recovering a Lost Commit with `git reflog`
`git reflog` records updates to the tip of branches (HEAD), allowing you to see the history of commits and other Git actions, even if the commit is no longer part of any branch or reference.

#### 1. View the recent HEAD changes:
```bash
git reflog
```
- This command will display a list of recent changes to the HEAD, including commits, merges, rebases, and resets.

#### 2. Identify the commit hash of the lost commit.
```bash
PS C:\ebooks\git-github-ebook-test> git reflog
4134ad2 (HEAD -> dev) HEAD@{0}: reset: moving to HEAD~1
73ac997 HEAD@{1}: commit: git reset example
4134ad2 (HEAD -> dev) HEAD@{2}: reset: moving to HEAD~1
bed2cc3 HEAD@{3}: commit: git reset example
4134ad2 (HEAD -> dev) HEAD@{4}: revert: Revert "revert"
56c9845 HEAD@{5}: commit: revert
3d87987 HEAD@{6}: merge vv1.0: Merge made by the 'ort' strategy.
28b146b HEAD@{7}: checkout: moving from main to dev
d207431 (tag: vv1.0, main) HEAD@{8}: checkout: moving from main to main
d207431 (tag: vv1.0, main) HEAD@{9}: merge release/v1.0: Merge made by the 'ort' strategy.
ca382f6 (origin/main) HEAD@{10}: checkout: moving from release/v1.0 to main
28b146b HEAD@{11}: checkout: moving from dev to release/v1.0
28b146b HEAD@{12}: checkout: moving from feature/feature-article to dev
28b146b HEAD@{13}: checkout: moving from dev to feature/feature-article
28b146b HEAD@{14}: reset: moving to HEAD
```
- Look through the output to find the commit you need to recover. Each entry is associated with a reference, such as `HEAD@{2}`, and a commit hash.

#### 3. Checkout or reset to the lost commit:
Once you've identified the commit hash, you can either checkout or reset to that commit.
- **Using `git checkout`:** This will move your HEAD to the specific commit, but it doesn't modify your working directory or staging area.
```bash
git checkout <commit-hash>
```

- **Using `git reset --hard`:** This will reset your HEAD and working directory to the specific commit, discarding any uncommitted changes.
```bash
git reset --hard <commit-hash>
```

### Example:
View the reflog to find the lost commit:
```bash
git reflog
```

Output example:
```bash
abc1234 HEAD@{2}: commit: Added new feature
```

Recover the commit by checking it out:
```bash
git checkout abc1234  # Restore the commit to your working directory
```

Or, if you want to reset your branch to this commit, use:
```bash
git reset --hard abc1234  # Move the branch pointer and working directory to the commit
```

### Finding Dangling Commits with `git fsck`
If you can't find the commit in the reflog, it might be "dangling," meaning it’s not referenced by any branch or tag but still exists in Git's database. You can search for these dangling commits using `git fsck`.

#### 1. Run `git fsck` to find dangling commits:
```bash
git fsck --lost-found
```
- This will list objects that are not part of any references, including dangling commits.

#### 2. Inspect the dangling commit(s):
Look for entries labeled "dangling commit" in the output, and use `git show` to inspect them.
```bash
git show hash-commit
```

### Example:
Find dangling commits with `git fsck`:
```bash
git fsck --lost-found
```

Example output:
```bash
dangling commit abc1234
```

Inspect the dangling commit:
```bash
git show abc1234
```

This will display the details of the commit, allowing you to decide if it’s the commit you want to recover.

## More About `git status`, `git log`, `git show` and `git diff`

Understanding `git status`, `git log`, and `git diff` helps in tracking changes effectively.

### `git status`
Shows the current state of the working directory and staging area.

#### Usage:
```bash
git status
```

### `git log`
Displays commit history.

#### Usage:
```bash
git log
```

### `git diff`
Shows changes between commits, branches, or the working directory.

#### Compare working directory with the last commit:
```bash
git diff
```

<!-- ## More About `git commit --amend`

- `git commit --amend` allows modifying the last commit.
- Useful for correcting messages or adding missed changes.

#### Example:
```bash
git commit --amend -m "Updated commit message"
``` -->

<!-- ## More About `git archive`

Used to create compressed archives of a repository.

#### Example:
```bash
git archive --format=zip HEAD > repo.zip
```  -->