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
#### 1. Check the commit you want to revert:
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

#### 2. Copy the hash and run `git revert`:
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
- **Mixed (`--mixed`)**: Resets the HEAD to a previous commit and removes the changes from the staging area, but leaves the changes in the working directory.
- **Hard (`--hard`)**: Completely removes the commit and all changes, both from the staging area and the working directory.

### `--soft` Example:
The `--soft` option undoes the last commit, but keeps the changes in the staging area, so you can easily modify the commit or change the commit message. This is useful if you want to redo a commit without losing the work you've done.

You go back to the `git add .` step.
```bash
git reset --soft HEAD~1 
```
- In this example, `HEAD~1` moves the HEAD back by one commit, all the changes remain staged, so you can re-commit them after making adjustments.


### `--mixed` Example:
The `--mixed` option resets HEAD to the specified commit, removes the changes from the staging area, but leaves them in the working directory. This is the default behavior of `git reset` if no mode is specified.

It is similar to `--soft`, the main difference is that with `--mixed` you go back before `git add .`.
```bash
git reset --mixed HEAD~1
```
- This command undoes the last commit and unstages the changes, but the changes remain in your working directory, so you can still modify them.

### `--hard` Example:
The `--hard` option resets both the staging area and the working directory to match the specified commit. This means all changes are lost and cannot be recovered unless you have backups or use `git reflog`.

Destructive action, caution here!
```bash
git reset --hard HEAD~1
```
- This will remove the last commit and all the changes associated with it, both in the staging area and the working directory.


## `git checkout`

`git checkout` can be used to undo changes in individual files or switch branches. We've talked about him only for branches since now.

`git checkout` is also used for undoing commits, but now `git switch` and `git restore` are recommended for these tasks.

### Usage to restore specific files:
`git checkout` can be used to undo changes in individual files and restore them to the last committed state.
```bash
git checkout -- filename.txt
```
- This command will discard any uncommitted changes in the `filename.txt` file and restore it to its last committed state.

The `--` is used to tell Git that you're referring to a file (not a branch) and you want to discard changes in the working directory, restoring the file to the state of the last commit.

### `git restore` Example:
`git restore` is the recommended command for restoring files, and it's more intuitive than using `git checkout` for this purpose.
```bash
git restore filename.txt
```
- This command will discard any uncommitted changes in the `filename.txt` file and restore it to the version from the last commit, just like `git checkout -- filename.txt`.

## Recovering Lost Commits
If you accidentally lose a commit in Git, you can recover it using commands like `git reflog` and `git fsck`. These tools help you identify and restore commits that seem to have been lost.

With sure, it's a type of command that you didn't use a lot, but you need to know that exists.

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
git checkout commit-hash
```

- **Using `git reset --hard`:** This will reset your HEAD and working directory to the specific commit, discarding any uncommitted changes.
```bash
git reset --hard commit-hash
```

### Example:
View the reflog to find the lost commit:
```bash
git reflog
```

Output example:
```bash
8b3dac5 (HEAD, dev) HEAD@{2}: commit: git checkout
4134ad2 HEAD@{3}: reset: moving to HEAD~1
73ac997 HEAD@{4}: commit: git reset example
4134ad2 HEAD@{5}: reset: moving to HEAD~1
bed2cc3 HEAD@{6}: commit: git reset example
4134ad2 HEAD@{7}: revert: Revert "revert"
56c9845 HEAD@{8}: commit: revert
3d87987 HEAD@{9}: merge vv1.0: Merge made by the 'ort' strategy.
```

Recover the commit by checking it out:
```bash
git checkout 73ac997
```

Or, if you want to reset your branch to this commit, use:
```bash
git reset --hard 56c9845 
```

If you run `git reflog` again you will see that all the changes are made as a new commit:
```bash
56c9845 (HEAD) HEAD@{0}: reset: moving to 56c9845
8b3dac5 (dev) HEAD@{1}: reset: moving to 8b3dac5
73ac997 HEAD@{2}: checkout: moving from dev to 73ac997
8b3dac5 (dev) HEAD@{3}: commit: git checkout
4134ad2 HEAD@{4}: reset: moving to HEAD~1
73ac997 HEAD@{5}: commit: git reset example
4134ad2 HEAD@{6}: reset: moving to HEAD~1
bed2cc3 HEAD@{7}: commit: git reset example
4134ad2 HEAD@{8}: revert: Revert "revert"
56c9845 (HEAD) HEAD@{9}: commit: revert
```

### Finding Dangling Commits with `git fsck`
If you can't find the commit in the reflog, it might be "dangling" meaning it’s not referenced by any branch or tag but still exists in Git's database. You can search for these dangling commits using `git fsck`.

Imagine that exists a lost commit in the repository, you can find with the command `git fsck`. The lost commits could happen when we forgot to merge branches and delete the work.

#### 1. Run `git fsck` to find dangling commits:
```bash
git fsck --lost-found
```
- This will list objects that are not part of any references, including dangling commits.

#### 2. Inspect the commits:
Look for entries labeled "dangling commit" in the output, and use `git show` to inspect them.
```bash
git show commit-hash
```

### Example:
Find dangling commits with `git fsck`:
```bash
git fsck --lost-found
```

Example output:
```bash
dangling commit 047885dbe5a76825fa1780cecb741f76eeb9ec35
dangling commit 18baee9d1b898ee1d82504174672b80d63aafa9a
dangling commit 227a6260d4d24c359aa5d4bcf667326c5cf10724
dangling tree 36e529c29f83cad089c8ddc57b7a1fa329564e87
dangling commit 413e484a74bef6b89674ecc6108f5f4364b9395f
dangling commit 726c4249600cb31b5bc8b52238faf3c3e31b4f68
dangling commit 73ac997c040ffda224e4a387614e2f860a8e0905
dangling commit 74a4b8ab890536d2ab8dacf076eaa64a5b24e486
dangling tree 96fc3be44051489ebc3303a66c07108bbcb563da
dangling commit a2d081673eb8bdd9f8e3159d787050c77116e901
dangling commit bed2cc3d74faff05c84ba21f84b29ab37357af63
dangling commit c2df1cab9005791812dd7efb690f9ce5f799bf70
dangling commit c8a104a4a311e3ee8cc2a696aeae5e4dc46cbeea
dangling commit fcde575ac34212c1187cee90604d35f0f6b00202
```

Inspect the dangling commit:
```bash
git show 047885dbe5a76825fa1780cecb741f76eeb9ec35
```

The return:
```bash
commit 047885dbe5a76825fa1780cecb741f76eeb9ec35
Author: Lorenzo Uriel <lorenzouriel394@gmail.com>
Date:   Sun Feb 16 21:01:01 2025 -0300

    Updated commit message

diff --git a/filename.txt b/filename.txt
index 8d1c8b6..91b27f5 100644
--- a/filename.txt
+++ b/filename.txt
@@ -1 +1,2 @@

+Lorenzo Uriel
\ No newline at end of file
```
- Display all the details of the commit, allowing you to decide if it’s the commit you want to recover.

## More About `git status`, `git log`, `git show` and `git diff`
Yes... it's more because we already use them above.

Understanding the commands `git status`, `git log`, `git show`, and `git diff` can help you track changes and managing your Git repository in a more smart way. 

With these commands you can check the current state of your repository, help you explore commit histories, and allow you to see the differences between various states of your files.

It's like a bunch of query statements.

### `git status`
`git status` provides an overview of the current state of the working directory and the staging area. It helps you track which changes have been staged, which are not, and which files are untracked.
```bash
git status
```

Example output:
```bash
HEAD detached from 73ac997
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md
        modified:   filename.txt
        modified:   filename2.txt
        modified:   filename3.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        filename3 copy.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
- Changes to be committed: These files have been staged and are ready to be committed.
- Untracked files: These files are not being tracked by Git yet.

### `git log`
`git log` shows the commit history of the repository, allowing you to explore previous commits, their messages, authors, and timestamps. You can also use various options to filter and format the log output.
```bash
git log
```

Example output:
```bash
commit 71333c330b93ffe20e02e6bac2b9a57ce15e355c (HEAD)
Author: Lorenzo Uriel <lorenzouriel394@gmail.com>
Date:   Mon Mar 10 21:56:23 2025 -0300

    oh yeah

commit 56c9845e9e0ff4298def3b693456f8857d82824b
Author: Lorenzo Uriel <lorenzouriel394@gmail.com>
Date:   Sun Mar 9 21:33:00 2025 -0300

    revert

commit 3d87987f33e66c859aa25f6a950995815c8caf50
Merge: 28b146b d207431
Author: Lorenzo Uriel <lorenzouriel394@gmail.com>
Date:   Wed Mar 5 23:14:00 2025 -0300

    show
```
- Commit hash: The unique identifier for the commit.
- Author: Who made the commit.
- Date: When the commit was made.
- Commit message: A brief description of the changes made in that commit.

You can also use `git log --oneline` for more resumed details:
```bash
git log --oneline
```

Example output:
```bash
5b07142 (HEAD) html example for git show
71333c3 oh yeah
56c9845 revert
3d87987 herge tag 'vv1.0' into dev Showw show
d207431 (tag: vv1.0, main) Merge branch 'release/v1.0'
28b146b Yes
0a91ea2 Updated commit message
ca382f6 (origin/main) filename3
db14708 new file
5a26f39 (tag: v1.0.0) first commit
```

### `git show`
`git show` allows you to view detailed information about a specific commit, including the commit message, author, date, and the changes made.

It was the command we use in the topic above.
```bash
git show 5b07142
```

Example output:
```bash
commit 5b071427e8369b85a56a5ee6b5388a2e2586306c (HEAD)
Author: Lorenzo Uriel <lorenzouriel394@gmail.com>
Date:   Mon Mar 10 22:02:09 2025 -0300

    html example for git show

diff --git a/README.md b/README.md
index 49d8b13..a71ae21 100644
--- a/README.md
+++ b/README.md
@@ -1,3 +1,3 @@
 "# git-github-ebook-test"

-git revert test
+git revert testfcfdefd
diff --git a/filename.txt b/filename.txt
index 8d1c8b6..8ebae4c 100644
--- a/filename.txt
+++ b/filename.txt
@@ -1 +1,2 @@

+sdfdfdfadf
\ No newline at end of file
diff --git a/filename2.txt b/filename2.txt
```
- This will show the changes made in the commit (the diff) along with other metadata.

### `git diff`
`git diff` shows the differences between various states of the repository, such as changes between the working directory and the last commit, between two commits, or between branches.

Compare working directory with the last commit:
```bash
git diff
```

Example output:
```bash
diff --git a/index.html b/index.html
index 64b907a..a24d290 100644
--- a/index.html
+++ b/index.html
@@ -3,7 +3,7 @@
 <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
-    <title>My First HTML Page</title>
+    <title>My Second HTML Page</title>
 </head>
 <body>
     <h1>Welcome to My First HTML Page</h1>
```
- This shows the changes between the working directory and the last commit. The `+` sign indicates a line added, and the `-` sign indicates a line removed.

#### Compare two commits:
You can also compare the changes between two commits by specifying their hashes:
```bash
git diff 5b07142 e0f5e31
```
- This shows the differences between the two specified commits.

Example output:
```bash
diff --git a/index.html b/index.html
index a24d290..685af61 100644
--- a/index.html
+++ b/index.html
@@ -3,7 +3,7 @@
 <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
-    <title>My Second HTML Page</title>
+    <title>My Third Example HTML Page</title>
 </head>
 <body>
     <h1>Welcome to My First HTML Page</h1>
```

#### Compare branches:
To see differences between branches, use:
```bash
git diff main dev
```
- This shows the differences between the two branches, helping you see what changes are in one branch but not the other.

Example output:
```bash
diff --git a/README.md b/README.md
index f3e1357..f70444d 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,3 @@
 "# git-github-ebook-test"
+
+git reset example
\ No newline at end of file
diff --git a/filename3.txt b/filename3.txt
index 8d1c8b6..3ad7dfd 100644
--- a/filename3.txt
+++ b/filename3.txt
@@ -1 +1,2 @@

+Changes on files
\ No newline at end of file
```

## More About `git commit --amend`
One day you made a big, beautiful commit message and 5 minutes later you find a code change and need to commit again?

Why not just commit to the same last commit if it's just a small change? `--amend` can help with this.

The `git commit --amend` command is used to modify the most recent commit in Git. It allows you to correct the commit message, add or remove changes from the commit, or even update both the changes and the message in one go.

This command is particularly useful when:
- You realize that the commit message needs to be improved.
- You forgot to include some changes in the commit.

### Usage:
```bash
git commit --amend
```

By default, running this command will open the commit editor to allow you to modify the commit message. You can also pass the `-m` option to directly update the commit message.

#### Example 1: Modify the Commit Message
If you want to update the message of the last commit, you can use:
```bash
git commit --amend -m "Updated commit message"
```
- This will replace the message of the last commit with the new one.

#### Example 2: Add Missed Changes
If you realize that you forgot to stage some changes for the last commit, you can:

1. Stage the changes you missed:
```bash
git add .
```

2. Amend the commit with the staged changes:
```bash
git commit --amend
```
- This will open the commit editor again, where you can modify the commit message if desired. If you don't want to change the message, simply save and close the editor.

The amended commit will now include both the original changes and the newly staged changes.

#### Example 3: Completely Replace the Commit (Message + Changes)
If you want to both change the commit message and the changes, stage the changes first and then run the `--amend` command:
```bash
git add .
git commit --amend -m "New commit message with updated changes"
```
- This will replace the last commit with the new changes and the new commit message.

***`git commit --amend`** rewrites the last commit, so it changes its commit hash. This can cause issues if the commit has already been pushed to a shared repository. It's recommended to only amend commits that haven't been pushed yet, or to use it cautiously if you have already shared your changes.*