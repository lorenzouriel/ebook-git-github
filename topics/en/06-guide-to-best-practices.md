# A Guide to Best Practices

You need to learn some best practices before making your next commit.

What is the best type of message? Or the best name for the branches?

We always seek to apply best practices in our projects. If you don't already do this, it's time to start.

Even more so when we work as a team, share repositories and have code reviews.

You know that commit that broke all the code and the message only said: "Now go!"? Well, that's what I'm talking about.

So what to do?

What are the best practices when it comes to Git & GitHub?

## Clear and Frequent Commits

With sure the most important and the first of the list: Write in a manner that people can understand!

Make small and frequent commits to maintain a clear change history.

Use descriptive and standardized commit messages explaining what was changed and why.

**Example:** 
```bash
git commit -m "fix: login issue by correcting password validation"
```

Avoid generic commits like only "fix" or "update." Prefer something with more details.

Make small commits, where each one addresses a single change. Stop making commits and writing a whole text explaining what changed, this is terrible when we need to revert.

### Tips for Commits Messages
What to write in your commit message?

I know you've had this question, especially when we make several changes and need to specify everything in a single commit.

I follow some practices that I consider good in my projects. They are:
- `feat: added support for automatic backup`
- `fix: adjusted data normalization`
- `revert: reverted change to the bank schema`
- `delete: removed table [old_logs]`
- `update: updated database structure`
- `config: adjusted database connection in .env`
- `ci: added migration step in the pipeline`
- `docs: documented table structure`
- `test: added tests for ETL functions`

The idea is to put at the beginning a description of what the commit is about, followed by a clear detail of what was accomplished.

Frequent commits are always better! Don't wait to do everything at once.

## Branch Management
Use branches to manage feature development, deploys, releases and other tasks. Adopt a workflow that is good for your team, such as:
- **Git Flow:** The most common and most popular way to work, divided by principal branches (`dev`, `main`) and secondary (`feature`, `release`, `hotfix`).
- **Trunk-Based Development:** The project is centralized in only one unique branch for all team, the `main` and we have the concept of `feature-branchs` for changes.

### Tips for Branches Names
And we always find ourselves with the same question, which title to put in this branch?

#### Main Branches
The default I see in the industry for main branches is:
- `dev` - `development`
- `qa` - `test`
- `main`

#### Change or Feature Branches
For change and secondary branches always specify the objective and add a descriptive message:
- `feature/add-backup-automation`
- `fix/fix-null-values-in-report`
- `hotfix/fix-production-database-issue`
- `refactor/normalize-user-table`
- `release/1.0.0`

A good tip is relate the task id and the task title, if your backlog supports:
- `feature/task544-add-backup-automation`
- `fix/task17-fix-null-values-in-report`

### Rebase
Another good tip when working with branches is the `git rebase` command. You can reorder or edit commits before merging. This helps maintain a linear and readable history:
```bash
git rebase -i HEAD~3  # Reorder or edit the last three commits interactively
```

*Avoid rebasing shared branches like `main` or `dev` to prevent conflicts and confusion for others.*

### Delete
Regularly delete old or outdated branches to keep the repository clean:

```bash
git branch -d feature/task544-add-backup-automation  # Delete a merged branch
git branch -D feature/task544-add-backup-automation  # Force delete an unmerged branch
```

## Use .gitignore
Always configure an appropriate `.gitignore` file for your project to avoid versioning unnecessary files.

Exclude build files, dependencies, credentials and every possible environment configurations.

I recommend you to use the [toptal site](https://www.toptal.com/developers/gitignore), he generates the most complete `.gitignore` files for every language. This is a [python example generated with toptal.](https://www.toptal.com/developers/gitignore/api/python)

You can also check the ready-made templates made by github in [github/gitignore repository](https://github.com/github/gitignore).

## Git Hooks
With Git Hooks you can automate rules and standards that need to be applied at various stages of your workflow. 

### Pre-commit Hooks
Use pre-commit hooks to run automated checks before changes are committed. These hooks can enforce code your pre-defined quality standards, some examples:
- Running linters to catch syntax errors or style.
- Executing unit tests to ensure changes don’t break the code.
- Validating commit messages to follow a consistent format.

Here you can detect errors early and prevent the developer from submitting any code that could affect the main project.

### Post-receive Hooks
Use post-receive hooks to automate tasks after changes are pushed to a remote repository. These hooks are ideal for:
- Updating staging or production environments automatically.
- Triggering CI/CD pipelines to deploy or test changes.
- Sending notifications to your team about new updates.

Of course, minimizing errors and creating an automatic initial deployment.


