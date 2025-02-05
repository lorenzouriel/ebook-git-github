# Working with Branches
## Creating and Managing Local Branches
**1. Create a new branch:**
```shell
git branch <branch-name>
```

**2. Switch to a branch:**
```shell
git checkout <branch-name>
```

**3. Create and switch to a new branch:**
```shell
git checkout -b <branch-name>
```

**4. List all branches:**
```shell
git branch
```

**5. Rename a branch:**
```shell
git branch -m <branch-name>
```

**6. Delete a branch:**
```shell
git branch -d <branch-name>
```

## Merging Branches
**1. Merge a branch into the current branch:**
```shell
git merge <branch-name>
```

### Resolving Merge Conflicts
During a merge, if there are conflicts, Git will pause the process and inform you of the conflicting files. Edit these files to resolve the conflicts, marked with:
```git
<<<<<<< HEAD
(changes in the current branch)
=======
(changes in the branch being merged)
>>>>>>> <branch-name>
```

After resolving the conflicts, mark the files as resolved:
```shell
git add .
```

Finish the merge:
```shell
git commit -m "Conflicting files resolved."
```

### Remote Branches and Branch Tracking
**1. List remote branches:**
```shell
git branch -r
```

**2. Create a branch tracking a remote branch:**
```shell
git checkout --track origin/<remote-branch-name>
```
- You only need to track if the remote branch does not exist in your local repository.

**3. Update remote branches:**
```shell
git fetch
```

**4. Merge changes from a remote branch into the current branch:**
```shell
git pull origin <remote-branch-name>

# Or just

git pull
```

## Workflow with Branches (Feature Branch, Hotfix and Release.)
**1. Feature Branch:**
- Create a new branch for the feature:
```shell
git checkout -b feature/<feature-name>
```

- Work on the feature and make commits.

- Merge the feature branch into the main branch (usually `main` or `dev`):
```shell
git checkout main
git merge feature/<feature-name>
```

**2. Hotfix Branch:**
- Create a new branch for the hotfix from the main branch:
```shell
git checkout -b hotfix/<hotfix-name> main
```

- Work on the hotfix and commit.

- Merge the hotfix branch into the main branch:
```shell
git checkout main
git merge hotfix/<hotfix-name>
```

- Merge the hotfix branch into the `dev` branch (if any):
```shell
git checkout dev
git merge hotfix/<hotfix-name>
```

**3. Release Branch:**
- Create a new branch for the release from the development branch:
```shell
git checkout -b release/<version> <branch-name>

# Code
git checkout -b release/1.0.0 dev
```

- Test and prepare the release, committing as needed.

- Merge the release branch into the main branch and tag the release:
```shell
git checkout main
git merge release/<version>
git tag -a v<version> -m "Release <version>"

# Code
git checkout main
git merge release/1.0.0
git tag -a v1.0.0 -m "Release 1.0.0"
```

- Merge the release branch back into the `dev` branch:
```shell
git checkout dev
git merge release/<version>
```
--