# Sync and Collaboration

## Setting Up Remote Repositories
**1. Add a remote repository:**
```shell
git remote add origin <remote-repository-url>
```
- Replace `<remote-repository-url>` with the URL of your remote repository (e.g., on GitHub, GitLab, or Bitbucket).

**2. Check the configured remote repositories:**
```shell
git remote -v
```

**3. Change the URL of a remote repository:**
```shell
git remote set-url origin <new-remote-repository-url>
```

**4. Remove a remote repository:**
```shell
git remote remove origin
```

## Pushing Changes to the Remote Repository (`git push`)
**1. Push changes to the main branch:**
```shell
git push origin main
```

**2. Push a specific branch to the remote repository:**
```shell
git push origin <branch-name>
```

**3. Push all local tags to the remote repository:**
```shell
git push --tags
```

## Getting Changes from the Remote Repository (`git pull` and `git fetch`)

**1. Update the local repository with changes from the remote repository and merge automatically:**
```shell
git pull origin main
```
- This is equivalent to `git fetch` followed by `git merge`.

**2. Get changes from the remote repository without merging:**
```shell
git fetch origin
```

**3. Merge changes pulled from the remote repository:**
```shell
git merge origin/main
```

## Working with Forks and Pull Requests

**1. Fork a repository:**
- On GitHub, GitLab, or Bitbucket, use the web interface to fork the desired repository.

**2. Clone the forked repository:**
```shell
git clone <url-of-forked-repository>
```

**3. Add an upstream repository to sync with the original repository:**
```shell
git remote add upstream <url-of-original-repository>
```
- The term "**upstream" is used to refer to the remote repository that is the official source for a project.** This is the main repository from which you typically want to sync updates.

**4. Sync your fork with the original repository:**
- Fetch changes from the original repository:
```shell
git fetch upstream
```

- Merge changes into the main branch:
```shell
git checkout main
git merge upstream/main
```

- Push changes to your fork on GitHub:
```shell
git push origin main
```

**5. Create a pull request:**
- On GitHub, GitLab, or Bitbucket, **use the web interface to create a pull request from your fork to the original repository.** Describe the changes you made and request review.

## Complete Flow Example
**1. Add Remote Repositories:**
```shell
git remote add origin <your-fork-url>
git remote add upstream <original-repository-url>
```

**2. Make Changes and Commit:**
```shell
git add .
git commit -m "My Contribution"
```

**3. Push Changes to the Fork:**
```shell
git push origin main
```

**4. Create a Pull Request:**
- On GitHub, **go to the original repository and click "New Pull Request".**
- ![example_pull_request](content/imgs/04/pull_request_01.jpg)

- In the **Pull Request** tab, click **New Pull Request**
- ![example_pull_request](content/imgs/04/pull_request_02.jpg)

- Select the branch that has changes (`compare:dev`) and the one you want to merge (`base:main`). Click on **Create Pull Request**
- ![example_pull_request](content/imgs/04/pull_request_03.jpg)

- GitHub will navigate to this tab and test again if the changes have no conflicts, after checking click on **Merge pull request**
- ![example_pull_request](content/imgs/04/pull_request_04.jpg)

- If you have this culture, you can delete the branch directly in the **Pull Request** step
- ![example_pull_request](content/imgs/04/pull_request_05.jpg)

**5. Sync with the Original Repository:**
- After applying the changes, you need to push to your local repository:
```shell
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

- Then, you can delete the branch from the local repository:
```shell
git checkout -d dev
```
---