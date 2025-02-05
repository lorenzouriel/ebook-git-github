# A Guide to Fundamental Concepts in Git & GitHub

Git is a powerful version control system that helps developers track changes, collaborate on projects, and manage code efficiently. In this guide, we’ll cover essential concepts and commands to get started with Git and GitHub.

## Introduction to Repositories and Concepts
A repository (repo) is a storage location where Git tracks changes in your project. It contains:

### What is a Repository?
- Files & Folders – Your project code
- Commits – Snapshots of code at different points
- Branches – Different versions of the code for development
- History – A record of all changes made

### Types of Repositories
- **Local Repository:** Stored on your computer
- **Remote Repository:** Hosted on platforms like GitHub, GitLab, Bitbucket for collaboration

Git enables working offline in a local repository and syncing changes with a remote repository when needed.

### Main Commands
These are the essential Git commands you’ll use frequently:

| Command                     | Description                                  |
|-----------------------------|----------------------------------------------|
| `git init`                  | Initializes a new Git repository            |
| `git clone <repo-url>`      | Copies (clones) a remote repo to your local machine |
| `git add <file>`            | Stages a file for commit                    |
| `git commit -m "message"`   | Saves changes to the repo                   |
| `git status`                | Shows the status of changes                 |
| `git log`                   | Displays commit history                     |
| `git branch`                | Lists branches                              |
| `git checkout <branch>`     | Switches branches                           |
| `git merge <branch>`        | Merges changes from another branch          |
| `git push origin <branch>`  | Pushes local changes to a remote repo       |
| `git pull origin <branch>`  | Pulls the latest changes from a remote repo |

### Creating a Local and Remote Repository
#### Create a Local Repository
1. Navigate to your project folder:
```bash
cd my-project
```
2. Initialize a new Git repository:
```bash
git init
```
3. This creates a `.git` folder where Git stores version control data.
4. Add files and commit:
```bash
git add .
git commit -m "Initial commit"
```

#### Create a Remote Repository on GitHub
1. Go to GitHub > New Repository
2. Name your repository and click Create
3. Link your local repo to GitHub:
```bash
git remote add origin https://github.com/user/repo.git
git branch -M main
git push -u origin main
```



## Concepts Related to Git
### Markdown

### Versioning










