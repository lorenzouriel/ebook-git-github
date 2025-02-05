# Best Practices
## Clear and Frequent Commits
#### Frequent Commits:
- Make small, frequent commits to make it easier to identify problems and revert specific changes.
- Each commit should represent a single, logical change to the code.
- Every change should have a commit.

#### Clear Commit Messages:
- Use descriptive, meaningful commit messages.
- The line should be a short, concise summary (50 characters or less), and you can add a more detailed description if necessary.
```shell
git commit -m "Fix bug in login function"
git commit -m "Add unit tests for authentication module"
```

## Using `.gitignore`
#### Creating and Using the `.gitignore` File:
- The `.gitignore` file is used to specify which files and directories should be ignored by Git.

- Common examples include local configuration files, build directories, and temporary files.

- You can use the [toptal](https://www.toptal.com/developers/gitignore) website to find complete and populated `.gitignore` files for your language.

Example of a `.gitignore` file:
```shell
# Logs
*.log

# Build directories
/build/
/dist/

# Configuration files
.env
.vscode/

# Temporary files
*.tmp
```

- To create or edit the `.gitignore` file, add it to the root of your repository.

## Branch Repositioning
#### Rebase instead of Merge:
Use `git rebase` to apply commits from one branch on top of another, creating a more linear history. 
```shell
git checkout feature-branch
git rebase main
```
- The `git rebase` command is used to merge changes from one branch into another, but in a different way than the `git merge` command. While `merge` creates a new `merge` commit, `rebase` reapplies the commits from one branch over the tip of another branch, resulting in a linear history.

Resolve conflicts if necessary and continue with:
```shell
git rebase --continue
```

#### Merge Branches:
Use `git merge` to combine changes from one branch into another, preserving the commit history.
```shell
git checkout main
git merge feature-branch
```

## Maintaining a Clean and Comprehensible History
#### Interactive Rebase to Clean Up History:
Use `git rebase -i` to reorder, edit, squash, or discard commits.
```shell
git rebase -i HEAD~n
```
- In the editor that opens, change `pick` to `squash` to combine commits.

Avoid unnecessary merge commits by using `git pull --rebase` instead of `git pull`.

## Automating Tasks with Git Hooks
#### Configure Git Hooks:
Git hooks are scripts that run automatically on certain events, such as before a commit or after a push.

Examples of hooks include `pre-commit`, `pre-push`, `post-commit`, and others.

Example of a `pre-commit` hook to check code style:
```shell
@echo off
# Pre-commit hook to run pytest

echo Running pytest
pytest

# if pytest fails, don't commit
if errorlevel 1 (
echo Tests failed
exit /b 1
)
```

Place the hook scripts in the `.git/hooks/` directory of your repository and make the scripts executable:
```shell
chmod +x .git/hooks/pre-commit
```

## Summary
- Clean and frequent commits make collaboration and code management easier.

- Using .gitignore keeps the repository clean of unnecessary files.

- Repositioning branches with proper rebasing and merging keeps the history readable and linear.

- Maintaining a clean history with tools like interactive rebasing avoids unnecessary complexity.

- Task automation with Git hooks ensures code quality and repository consistency.
---