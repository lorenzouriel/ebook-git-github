# A Guide to Workflow Types
What is a workflow? And why should you use one?

That's what I want to explain today. I'm sure you'll start using it today.

A workflow defines how you and your team can collaborate using Git and GitHub. Choosing the right workflow will depend on how your team is structured, the complexity of the project, and your strategies for releasing a new version.

I'll explore the most common workflows and use cases.

## Trunk-Based Development
The most used, with sure. You probably just used this and didn't know that has a name.

But how it works?

Developers work directly on the `main` branch or create **short-lived feature branches.** All changes are merged into `main` multiple times a day.

It happens frequent integration that minimizes merge conflicts. With this we can have fast delivery, real-time collaboration and fewer merge conflicts.

### Workflow Steps
1. Start work:
```bash
git checkout -b feature-article
```

2. Make changes and push frequently:
```bash
git commit -m "Finish Article"
```

3. Merge the branch
```bash
git checkout main
git merge feature-article
git push origin main
```

### Diagram
![trunk-based](/topics/imgs/07-guide-workflow-types/trunk-based.png)

## GitFlow
Instead of having just one principal branch, we always have two, the `main` and the `dev`. 

Based on `dev` we can always create another branchs for different purposes, like:
- `feature branches`: Created from `dev`, merged back when complete.
- `release branches`: Created from `dev` when preparing for a release.
- `hotfix branches`: Created from `main` to fix urgent issues and merged into both `main` and `dev`.

The role of the `main` always stores production code and `dev` integrates all feature branches. We develop into `dev` branch to stop using production code.

Gitflow is the best option for CI/CD purposes.

### Workflow Steps
1. Initialize GitFlow:
```bash
git flow init
```

When initialize you will answers a small questionary to start the project:
```bash
Which branch should be used for bringing forth production releases?
   - dev
   - main
Branch name for production releases: [main]

Which branch should be used for integration of the "next release"?
   - dev
Branch name for "next release" development: [dev] 

How to name your supporting branch prefixes?
Feature branches? [feature/]
Bugfix branches? [bugfix/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? [v] 
Hooks and filters directory? [C:/ebooks/git-github-ebook-test/.git/hooks]
```

The `git flow init` itself will create all the structure.

2. Start a new feature:
```bash
git flow feature start feature-article
```
- This action creates a new feature branch based on `dev` and switches to it

3. Finish the feature:
```bash
git flow feature finish feature-article
```
- Merges `feature-article` into `dev`
- Removes the feature branch
- Switches back to `dev` branch

4. Publish a feature:
```bash
git flow feature publish feature-article
```
- This command publishes the resource itself to the remote repository for other users.

5. Create a release branch:
```bash
git flow release start v1.0
```
- It creates a release branch created from the `dev` branch.

6. Finish & deploy the release:
```bash
git flow release finish 'v1.0'
```
- Merge the `release` branch into `main`
- Tag the `release` with the name.
- Merge the `release` branch into `dev` again
- Then, removes the `release` branch 

The prompt message are as follows:
```bash
C:\ebooks\git-github-ebook-test>git flow release finish 'v1.0'
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
Merge made by the 'ort' strategy.
Already on 'main'
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)
Switched to branch 'dev'
Merge made by the 'ort' strategy.
Deleted branch release/v1.0 (was 28b146b).

Summary of actions:
- Release branch 'release/v1.0' has been merged into 'main'
- The release was tagged 'vv1.0'
- Release tag 'vv1.0' has been back-merged into 'dev'
- Release branch 'release/v1.0' has been locally deleted
- You are now on branch 'dev'
```

If you want to know more about the commands, I recommend this [Gitflow cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/index.html).

### Diagram
![gitflow](/topics/imgs/07-guide-workflow-types/gitflow.png)

## Feature Branch
The core is for teams working on multiple features simultaneously, here each feature is developed in a separate branch and feature branches merge back into `main` after review. 

The unique process here is create a `feature` branch and the merge to the `main` after a review.

### Workflow Steps
1. Create a feature branch:
```bash
git checkout -b feature-article
```

2. Work and commit changes:
```bash
git add .
git commit -m "Added Feature Branch Topic"
```

3. Push the branch and open a Pull Request:
```bash
git push origin feature-article
```

4. After approval, merge into `main` on the remote and local repository.

### Diagram
![feature-branch](/topics/imgs/07-guide-workflow-types/feature-branch.png)

## Forking Workflow
Developers fork a repository instead of working directly on it. Recommended and most used on Open-Source projects.

They clone, create a branch, and push their changes to their own fork. After all this, the changes are submitted as a **Pull Request (PR).**

### Workflow Steps
1. Fork the repository on GitHub.

2. Clone the forked repository:
```bash
git clone https://github.com/lorenzouriel/ebook-git-github.git
```

3. Create a branch and make changes:
```bash
git checkout -b feature-article
git add .
git commit -m "Added feature article"
git push origin feature-article
```

4. Submit a Pull Request to the original repository.

### Diagram 
![forking-workflow](/topics/imgs/07-guide-workflow-types/forking-workflow.png)

By learning this, you will be able to decide which workflow best suits you and your team, remembering that in many cases we already use one without even realizing it.