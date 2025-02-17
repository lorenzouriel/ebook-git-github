# A Guide to Work with Branches

So, you already know what a branch is and why you should have one. But now, how to work with them?

Let's see!

## What is a Git Branch?

**A Git branch is an independent line of development within a repository.** Think of it as a separate workspace where you can make changes without affecting the main (or default) branch. Branches allow developers to work on new features, bug fixes, or experiments without disrupting the actual version of the project.

## Why Use Branches?
Branches provide several benefits in a development workflow:
- **Isolation:** Keep different tasks (features, bug fixes, experiments) separate.
- **Collaboration:** Multiple developers can work on different branches without interfering with each other.
- **Safe Experimentation:** Test changes without affecting the production code.
- **Version Control:** Easily roll back or switch between different versions of the project.

In Git, the default branch is usually called main or master. However, new branches can be created for various purposes, such as:
- **Feature branches (`feature/new-ui`):** Used for developing new functionalities.
- **Bugfix branches (`hotfix/login-fix`):** Used for fixing issues in production.
- **Release branches (`release/v1.2.0`):** Used to prepare stable versions for deployment.

## Creating and Managing Local Branches
Branches in Git allow you to work on new features, bug fixes, or experiments without affecting the main codebase. Here’s how to create, switch, rename, and delete branches efficiently.

### 1. Create a New Branch
```shell
git branch feature/create-chapter
```
- This creates a new branch named `feature/create-chapter` but does not switch to it.
- Useful when you need to prepare multiple branches but don’t want to switch immediately.

### 2. Switch to a Branch
```shell
git checkout feature/create-chapter
```
- This moves you to the specified branch so you can start coding.

**Modern Alternative:** Since Git 2.23+, use `git switch`:
```shell
git switch feature/create-chapter
```

It’s a cleaner and safer alternative to `checkout`.

### 3. Create and Switch to a New Branch (Shortcut)
```shell
git checkout -b feature/create-chapter
```
- Creates a new branch and switches to it immediately.
- Saves time by combining two commands into one.

**Modern Alternative:**
```shell
git switch -c feature/create-chapter
```

More intuitive and recommended for newer Git versions.

### 4. List All Branches
```shell
git branch
```

- Displays all local branches. The current branch is marked with `*`.
```shell
* dev/ebook-v2
  main
  feature/add-search
  bugfix/fix-typo
```
- This helps you track available branches and navigate between them.

To list remote branches as well:
```shell
git branch -a
```

### 5. Rename a Branch
```shell
git branch -m feature/create-chapter feature/create-chapter-branch
```
- Renames the branch `feature/create-chapter` to `feature/create-chapter-branch`.

If you're already on the branch you want to rename:
```shell
git branch -m new-branch-name
```

### 6. Delete a Local Branch (Safely)
```shell
git branch -d feature/create-chapter-branch
```
- Deletes the branch only if it’s already merged into another branch.
- If it has unmerged changes, Git will prevent deletion to avoid data loss.

### 7. Force Delete a Branch (Dangerous)
```shell
git branch -D feature/create-chapter-branch
```
- This deletes the branch unconditionally, even if it has unmerged changes.
- Use carefully to avoid losing important work.

### Best Practices for Managing Branches
1. Use clear and descriptive branch names (`feature/add-login`, `bugfix/fix-typo`).
2. Delete old branches to keep your repository clean.
3. Use `-d` instead of `-D` unless you're sure you want to force-delete.
4. Regularly push branches to remote (`git push origin branch-name`) to prevent accidental loss.

## Merging Branches
In Git, **`merge` is the process of integrating changes from one branch into another.** It is commonly used to combine updates from different development branches into a main branch, like `main` or `develop`.

### 1. Merge a Branch into the Current Branch
To merge changes from another branch into your current branch:
```shell
git merge feature/create-chapter-branch
```
- This integrates the changes from feature/create-chapter-branch into the branch you are currently on.
- If no conflicts exist, Git will automatically complete the merge.

Ensure you are on the correct branch before merging:
```shell
git checkout main  # or git switch main
git merge feature/create-chapter-branch
```

### 2. Resolving Merge Conflicts
During a merge, if there are conflicts, Git will pause the process and inform you of the conflicting files. Edit these files to resolve the conflicts, marked with:
```shell
<<<<<<< HEAD
(changes in the current branch)
=======
(changes in the branch being merged)
>>>>>>> main
```
- The HEAD section represents changes from your current branch.
- The section below `=======` comes from the branch being merged.

#### Steps to Resolve Conflicts:
1. Open the conflicting file(s) in a text editor.
2. Manually edit and keep the correct version of the code.
3. Mark the files as resolved:
```shell
git add .
```
4. Complete the merge with a commit:
```shell
git commit -m "Conflicting files resolved."
```

To abort a merge and return to the previous state:
```shell
git merge --abort
```

### Types of Git Merges
Git supports different merging strategies depending on whether branches have diverged.

#### 1. Fast-Forward Merge (No Divergence)
A fast-forward merge happens when the branch being merged is ahead of the current branch without any changes on the current branch.

Git moves the branch pointer forward instead of creating a merge commit.

**Example:**
```shell
git checkout main
git merge feature/create-chapter-branch
```
-  This works when `main` has not changed since `feature/create-chapter-branch` was created.

#### 2. Three-Way Merge (Diverging Branches)
A three-way merge occurs when the two branches have different histories and cannot be fast-forwarded.

Git creates a new merge commit to combine the changes.
```shell
git checkout main
git merge feature/create-chapter-branch
```

You will see a commit message like:
```shell
Merge branch 'feature/create-chapter-branch' into main
```

### Best Practices for Merging
1. Always pull the latest changes before merging.
2. Test your code after merging to ensure everything works.
3. Use feature branches for development to keep `main` stable.
4. Delete merged branches to keep the repository clean.

## Rebasing Branches
Rebasing is a powerful Git feature that **allows you to integrate changes from one branch into another by moving your branch to the latest state of the target branch.** Unlike merging, which creates a new merge commit, **rebasing replays your commits on top of the latest changes, keeping the commit history cleaner.**

When to use rebase?
- To keep a feature branch up to date with the main branch.
- To clean up the commit history before merging.
- To rewrite commit history for better readability.


### 1. Rebase a Branch onto Another Branch
```shell
git checkout feature/create-chapter-branch
git rebase main
```

This updates `feature/create-chapter-branch` with the latest commits from `main`, ensuring it is based on the most recent changes.

*⚠ If conflicts occur during rebasing, Git will stop and ask you to resolve them before continuing.*

### 2. Abort an Ongoing Rebase

If something goes wrong during rebasing and you want to cancel the process, use:
```shell
git rebase --abort
```

This restores your branch to the state before you started the rebase.

### 3. Continue an Interrupted Rebase After Resolving Conflicts
When a conflict occurs, Git pauses the rebase and asks you to resolve conflicts manually in the affected files.

After fixing the conflicts, stage the resolved files:
```shell
git add .
```

Then, continue the rebase:
```shell
git rebase --continue
```

Git will continue applying the remaining commits. If another conflict occurs, repeat the process until the rebase is complete.

### 4. Interactive Rebase (modify commit history)
To edit, reorder, squash, or remove commits, use interactive rebase:
```shell
git rebase -i HEAD~3
```

`HEAD~3` means you are interacting with the last 3 commits.

After running this command, Git opens an interactive editor with options like:
- `pick` → Keep the commit as-is.
- `reword` → Change the commit message.
- `edit` → Modify the commit contents.
- `squash` → Merge commits together.
- `drop` → Delete a commit.

Example of an interactive rebase editor window:
```shell
pick 123abc filename3
squash 456def commit
pick 789ghi first commit

# Rebase db14708..ca382f6 onto db14708 (1 command)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
~ 
.git/rebase-merge/git-rebase-todo [unix] (20:33 16/02/2025)  
```

This will squash the second commit into the first one, combining their changes.

### Best Practices for Rebasing:
- Always rebase local branches before merging to keep history clean.
- Avoid rebasing shared branches (`main`, `dev`) as it rewrites commit history.
- Use `git rebase --interactive` to rewrite history in an organized way.
- If unsure, create a backup branch before rebasing.

## Remote Branches and Branch Tracking
Remote branches are versions of your branches stored on a remote repository (e.g., GitHub, GitLab, Bitbucket). These branches allow collaboration between multiple developers by keeping their local repositories in sync with the remote.

### Why use remote branches?
- To collaborate with others by pushing and pulling changes.
- To keep a backup of your work in a central repository.
- To manage different environments (`main`, `dev`, `staging`).


### 1. List Remote Branches
To see all branches stored in the remote repository:
```shell
git branch -r
```

- This lists only remote branches, prefixed by `origin/`.

To list both local and remote branches:
```shell
git branch -a
```

This helps check which branches exist locally and remotely.

### 2. Create a Branch Tracking a Remote Branch
If you want to work on a remote branch locally, use:
```shell
git checkout --track origin/dev
```
- This creates a local branch that automatically tracks the remote one.

The return will be:
```shell
branch 'dev' set up to track 'origin/dev'.
Switched to a new branch 'dev'
```

This is useful when Git doesn’t auto-track the branch.

### 3. Update Remote Branches
Fetching updates from the remote repository ensures you have the latest branch list:
```shell
git fetch
```
- This downloads remote changes but doesn’t apply them to your working directory.

#### 4. Merge Changes From a Remote Branch Into the Current Branch
To pull the latest updates from a remote branch into your local branch:
```shell
git pull origin main
```

This is equivalent to running:
```shell
git fetch
git merge origin/main
```

If the branch is already tracking `origin/main`, you can simply run:
```shell
git pull
```

*⚠ If conflicts occur, resolve them manually and commit the changes.*


### 5. Push a New Local Branch to the Remote Repository
After creating a new branch locally, push it to the remote repository:
```shell
git push -u origin dev
```
- The `-u` flag sets up tracking, so future `git pull` and `git push` commands can be run without specifying the remote branch.

### 6. Delete a Remote Branch
If a remote branch is no longer needed, delete it using:
```shell
git push origin --delete dev
```
- This removes `origin dev` from the remote repository.

To delete a local reference to the deleted remote branch:
```shell
git remote prune origin
```

### Best Practices for Remote Branch Management
1. Use descriptive branch names (`feature/login`, `bugfix/navbar-issue`).
2. Always fetch before merging to avoid conflicts.
3. Prune deleted branches regularly
4. Don’t push work-in-progress branches unless necessary.


## Stashing Changes
Git stash **allows you to temporarily save uncommitted changes without committing them.** This is useful when you need to:
- Switch branches without committing incomplete work.
- Keep your working directory clean while pulling changes.
- Save temporary work that you’re not ready to commit.

By stashing, Git stores your changes safely so you can retrieve them later.

### 1. Stash Uncommitted Changes
To stash all modified and staged files:
```shell
git stash
```
- This removes changes from the working directory and saves them in a stack.

To stash with a custom message:
```shell
git stash push -m "Fixing ETL"
```
- Helps you identify what each stash contains.

### 2. List Stashed Changes
To view all saved stashes:
```shell
git stash list
```
-  Each stash entry is labeled as `stash@{n}`, where `n` is its index.

**Example output:**
```shell
stash@{0}: On main: Fixing ETL
stash@{1}: On dev: Debugging API issue
```
- The latest stash is always `stash@{0}`.

### 3. Apply the Latest Stashed Changes
To apply the most recent stash without removing it from the stash list:
```shell
git stash apply
```
- This restores the stashed changes but keeps them in the stash.

To apply a specific stash:
```shell
git stash apply --index 2
```
-  Replace `2` with the desired stash index.

### 4. Apply and Remove the Latest Stashed Changes
To restore and remove the most recent stash:
```shell
git stash pop
```

To pop a specific stash:
```shell
git stash pop --index 1
```

- This removes `stash@{1}` after applying its changes.

### 5. Drop a Specific Stash
To delete a specific stash without applying it:
```shell
git stash drop --q 1
```
- Removes `stash@{1}` from the stash list.

### 6. Clear all Stashes
To delete all stashes at once:
```shell
git stash clear
```
- Use with caution—this permanently deletes all stashed changes.

### 7. Create a New Branch From a Stash
To create a branch with the stashed changes:
```shell
git stash branch feature-fix
```
-  This creates a new `feature-fix` branch from the most recent stash and applies the stash.

### Best Practices for Stashing
1. Use meaningful stash messages.
2. Apply stash before switching branches if necessary.
3. Clear old stashes to keep your repository clean.
4. Use stash branches for complex changes.


## Workflow with Branches (Feature Branch, Hotfix, and Release)
This guide outlines the typical workflow using Git branches for features, hotfixes, and releases. It ensures that development, bug fixes, and release processes are streamlined.

### 1. Feature Branch
Feature branches allow you to work on new features independently without affecting the main codebase.

- Create a new branch for the feature:
```shell
git checkout -b feature/create-chapter-branch
```
- Work on the feature and make commits, regularly commit your changes as you progress.
- Merge the feature branch into the main branch (`main` or `dev`).
```shell
git checkout main
git merge feature/create-chapter-branch
```

### 2. Hotfix Branch
Hotfixes are used for urgent bug fixes in the production environment, typically based on the main branch.

- Create a new branch for the hotfix from the main branch:
```shell
git checkout -b hotfix/main-app-filter main
```
- Work on the hotfix and commit.
- Merge the hotfix branch into the main branch:

```shell
git checkout main
git merge hotfix/main-app-filter main
```

- Also merge the hotfix into the `dev` branch: If you have a `dev` branch, ensure that the `hotfix` is merged there too, to keep the development branch up to date.
```shell
git checkout dev
git merge hotfix/main-app-filter main
```

### 3. Release Branch
Release branches are created for preparing a new version of the software for production. They allow for testing, final tweaks, and versioning.

- Create a new release branch from the dev branch: The release branch should be based on the dev branch to include all the new features.
```shell
git checkout -b release/1.0.0 dev
```

- Test and prepare the release, committing as needed. Make final adjustments, perform testing, and commit any necessary changes.
- Merge the release branch into the main branch and tag the release: After testing, merge the release branch into main and tag it with the version number to mark the official release.

```shell
git checkout main
git merge release/1.0.0
git tag -a v1.0.0 -m "Release 1.0.0"
```

- Merge the release branch back into the dev branch: To ensure any final changes made during the release process are reflected in the development branch, merge the release branch back into dev.
```shell
git checkout dev
git merge release/1.0.0
```

### Best Practices for Workflows
1. Use Descriptive Branch Names
2. Keep Branches Short-Lived
3. Commit Frequently and Logically
4. Keep the main Branch Stable
5. Use dev for Ongoing Development
6. Merge Instead of Direct Pushes to main or dev
7. Use Tags for Releases
8. Ensure Proper Testing on Release Branches
9. Clean Up Branches After Merging

## Cherry-Picking Commits
Cherry-picking **allows you to selectively apply specific commits from one branch to another.** Instead of merging or rebasing an entire branch, you can pick only the commits you need.

This is useful when:
- A bug fix is in a feature branch and needs to be applied to main.
- A commit from another developer's branch should be added to yours.
- A commit was mistakenly added to the wrong branch and needs to be moved.


### 1. Apply a Specific Commit From Another Branch
To apply a commit from another branch to your current branch:
```shell
git cherry-pick a1b2c3d
```

- This applies commit with the hash `a1b2c3d` to your current branch.

### 2. Apply Multiple Commits
To cherry-pick multiple commits in one command:
```shell
git cherry-pick a1b2c3d e4f5g6h
```

- This applies both commits in sequence.

### 3. Abort a cherry-pick Operation
If you encounter a conflict and want to cancel the operation:
```shell
git cherry-pick --abort
```

- This restores your branch to the state before you started cherry-picking.

#### 4. Cherry-Picking Without Committing
If you want to apply a commit’s changes without committing:
```shell
git cherry-pick -n a1b2c3d
```
- This applies the changes, but doesn’t create a commit.
- You can modify the files before committing manually.

### 5. Cherry-Picking with a Custom Commit Message
To use a custom message instead of the original commit message:
```shell
git cherry-pick -e a1b2c3d
```

- This opens an editor where you can modify the commit message.

### Best Practices for Cherry-Picking
1. Ensure you're on the correct branch before cherry-picking.
2. Use cherry-picking can lead to duplicate commits.
3. Verify commit history after cherry-picking to avoid conflicts.
4. Consider merging or rebasing instead of cherry-picking when appropriate.

## Undoing Changes
Sometimes, mistakes happen, and you need to undo changes in Git. Depending on the scenario, you might want to:
- Keep changes staged while undoing a commit.
- Completely erase a commit and its changes.
- Revert a commit while keeping history intact.
- Restore files to a previous state.

### 1. Undo the Last Commit (Keep Changes Staged)
If you want to undo the last commit but keep the changes staged:
```shell
git reset --soft HEAD~1
```
- The commit is undone, but changes remain in the staging area.
- Useful when you accidentally committed too soon and want to modify the commit before pushing.

**Example:**
```shell
git reset --soft HEAD~1
git commit -m "Updated commit message"
```

#### 2. Undo the Last Commit (Discard Changes)
If you want to undo the last commit and discard all changes:
```shell
git reset --hard HEAD~1
```
- This completely removes the commit and its changes.

**Example:**
```shell
git reset --hard HEAD~1
git log --oneline 
```

### 3. Restore a Deleted File
If you accidentally deleted a file and haven't committed the deletion yet:
```shell
git checkout -- filename.txt
```

- This restores the file to its last committed state.

### 4. Reset a File to the Last Committed State
If a file has been modified but not staged and you want to discard the changes:
```shell
git checkout HEAD -- filename.txt
```
- This restores the file to its last committed version, discarding local modifications.

### 5. Revert a Commit
If you want to undo a commit but keep history intact:
```shell
git revert 0a91ea2
```
- This creates a new commit that reverses the changes from the specified commit.
- Unlike `reset`, it does not remove history, making it safer for shared repositories.

### 6. Undo a Pushed Commit
If you accidentally pushed a commit and need to undo it before others pull it:
```shell
git reset --hard HEAD~1
git push --force
```
- *⚠️ `git push --force` overwrites history and can cause problems if others have already pulled the commit.*

If the commit has already been shared, use revert instead:
```shell
git revert 0a91ea2
git push
```

#### 7. Undo All Local Changes
If you want to reset everything to the last committed state:
```shell
git reset --hard HEAD
```
- This removes all uncommitted changes. Use with caution.

### Best Practices for Undoing Changes
- Use `reset --soft` when you want to redo a commit but keep your changes staged.
- Use `reset --hard` with caution it deletes changes permanently.
- Use `revert` instead of `reset` when working in a shared repository.
- Always double-check commit history (`git log --oneline`) before making destructive changes.