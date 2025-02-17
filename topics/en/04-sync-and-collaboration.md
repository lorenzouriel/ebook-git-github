# A Guide to Synchronization and Collaboration

Here is the main point for using GitHub, synchronization and collaboration between teams.

Or personal projects with a friend. Focus on using it this way and you will understand how functional it is.

## Setting Up Remote Repositories
Remote repositories are versions of your project hosted on the internet or network, allowing multiple developers to collaborate. They serve as the central hub for storing and sharing project changes.

To work with remote repositories, you need to add, modify, or remove them as needed. Below are the key commands for managing remote repositories:

### 1. Add a Remote Repository
```bash
git remote add origin https://github.com/lorenzouriel/ebook-git-github.git
```
- Replace with the actual URL of your remote repository.

### 2. Verify Configured Remote Repositories
```bash
git remote -v
```
- This command lists all configured remote repositories along with their fetch and push URLs.

### 3. Change the URL of a Remote Repository
```bash
git remote set-url origin https://github.com/lorenzouriel/ebook-git-github.git
```
- Useful when changing the remote location, such as migrating to a different provider.

### 4. Remove a Remote Repository
```bash
git remote remove origin
```
- This removes the connection to the specified remote repository.

## Pushing Changes to the Remote Repository (`git push`)
Once you've made and committed changes locally, you need to push them to the remote repository.

### 1. Push Changes to the Main Branch
```bash
git push origin main
```
- Sends the local `main` branch updates to the remote repository.

### 2. Push a Specific Branch to the Remote Repository
```bash
git push origin dev
```
- Replace `dev` with the name of the branch you want to push.

### 3. Push all Local Tags to the Remote Repository
```bash
git push --tags
```
- Sends all locally created tags to the remote repository.

## Getting Changes from the Remote Repository (`git pull` and `git fetch`)

To stay up to date with remote changes, you can pull or fetch updates.

### 1. Update your Local Repository with the Latest Changes and Merge Automatically
```bash
git pull main
```

- Equivalent to `git fetch` followed by `git merge`, it downloads and integrates remote changes.

### 2. Fetch Changes from the Remote Repository Without Merging
```bash
git fetch
```

- Downloads updates but does not apply them automatically.

### 3. Merge Fetched Changes Manually
```bash
git merge
```

- Merges the fetched updates into your local branch.

## Removing Local and Remote Repositories
### 1. Removing a Repository Locally
To delete a Git repository from your local machine, you can remove the directory where it is stored. Be cautious, as this will remove all files and commit history within the repository.
```bash
# Using Bash (Linux/macOS)
rm -rf /path/to/your/repository
git commit -m "Remove tests_git directory"
git push

# Using PowerShell (Windows)
git rm -r --cached /projects/portfolio/tests_git
Remove-Item -Path "C:\Projects\portfolio\tests_git" -Recurse -Force
git commit -m "Remove tests_git directory"
git push
```

### 2. Deleting Remote Repositories on GitHub
To delete a remote repository on GitHub, follow these steps:
1. Navigate to the repository page on GitHub.
2. Go to the Settings section of the repository.
- ![delete_repository](/topics/imgs/05/delete_repository.jpg)
3. Scroll down to find the Delete this repository option.
- ![delete_repository_2](/topics/imgs/05/delete_repository_2.jpg)
4. Confirm the deletion by entering your password or using GitHub Mobile.


## Working with Tags

## Working with Releases

## Working with Forks and Pull Requests
Forking a repository allows you to contribute to a project without modifying the original repository directly. It's a way to contribute with Open-Source projects.

### 1. Fork a Repository
On GitHub  use the web interface to fork the desired repository.
- ![fork](/topics/imgs/04/fork.png)

### 2. Clone the Forked Repository
```bash
git clone https://github.com/lorenzouriel/opentelemetry-python-contrib.git
```
- This creates a local copy of your forked repository.

### 3. Add an Upstream Repository to Sync With the Original Project
```bash
git remote add upstream https://github.com/open-telemetry/opentelemetry-python-contrib.git
```
- The **upstream** repository refers to the original repository from which you forked.

### 4. Sync your Fork With the Original Repository
Fetch changes from the upstream repository:
```bash
git fetch upstream
```

- Merge updates into your main branch:
```bash
git checkout main
git merge upstream/main
```

- Push the updates to your fork:

```bash
git push origin main
```

### 5. Create a Pull Request
- On GitHub, **go to the original repository and click "New Pull Request".**
- Compare changes between your fork and the original repository.
- Click **Create Pull Request** and add a descriptive message.
- Once reviewed and approved, the maintainer can merge your contribution.

## Complete Flow Example
This example demonstrates a full workflow for contributing via a fork and pull request:

### 1. Add Remote Repositories
```bash
git remote add origin https://github.com/lorenzouriel/opentelemetry-python-contrib.git
git remote add upstream https://github.com/open-telemetry/opentelemetry-python-contrib.git
```

### 2. Create a New Branch, Make Changes, and Commit
```bash
git checkout -b my-feature
# Modify files

git add .
git commit -m "Added a new feature"
```

### 3. Push Changes to Your Fork
```bash
git push origin my-feature
```

### 4. Create a Pull Request via GitHub
- Navigate to the original repository.
- Click "New Pull Request".
- Select your branch (`my-feature`) and the main branch of the original repository.
- Add a description and submit the pull request.

**5. Sync with the Original Repository After a Merge:**
Update your local repository with the latest changes:
```bash
git fetch upstream
git checkout main
git merge upstream/main
```

- Push the synced main branch back to your fork:
```bash
git push
```

**6. Delete the Merged Branch:**
```bash
git branch -d my-feature
```

- Optionally, delete the remote branch as well:
```bash
git push origin --delete my-feature
```

This workflow ensures synchronization and collaboration while contributing to open-source projects.

## Tags and Releases
### 1. Create a Tag
Tags are used to mark specific points in the commit history, such as releases.
```bash
git tag v1
```

### 2. Create an Annotated Tag
Annotated tags include additional metadata, such as the tag message, making them ideal for releases.
```bash
git tag -a v1 -m "Version 01"
```

### 3. Push a Tag to the Remote Repository
After creating a new tag, push it to the remote repository:
```bash
git push origin v1
```

### 4. Push All Local Tags to the Remote Repository
To push all tags at once:
```bash
git push --tags
```

### 5. List All Tags
To list all tags in your local repository:
```bash
git tag
```

### 6. Delete a Tag Locally
To delete a tag from your local repository:
```bash
git tag -d v1
```

### 7. Delete a Tag in the Remote Repository
To delete a tag from the remote repository:
```bash
git push origin --delete v1
```

### 8. Create a Release on GitHub
To create a release on GitHub:
1. Navigate to the Releases section of the repository.
2. Click **Create a New Release**
- ![release](/topics/imgs/05/release.jpg)
3. Fill in the release information, associate a tag, and click **Publish a New Release**:
- ![release_2](/topics/imgs/05/release_2.jpg)
4. Your releases will be organized in the Releases section under the **Code** tab:
- ![release_3](/topics/imgs/05/release_3.jpg)

---

## Block Main From Directly Push

## More About the git remote Command