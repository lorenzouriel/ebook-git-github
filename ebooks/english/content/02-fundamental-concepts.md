# A Guide to Fundamental Concepts
Without understanding the fundamentals, its history and what it makes up. It doesn't make sense for a man to continue walking the path.

Okay, I didn't need to say that catchphrase. But we'll focus on this chapter as a general introduction to what constitutes Git & GitHub.

## Introduction to Repositories and Concepts

A **repository** is where a project's files, history, and changes are stored. It can be:

- **Remote:** Hosted on platforms like GitHub, GitLab, or Bitbucket.
- **Local:** Stored directly on the developer's machine.

## **Main Concepts**

### **Branches**
Branches allow developers to work on different features or fixes without affecting the main codebase. The primary branch is usually called **main**, but you can create new branches for specific tasks.
- **Example:** Suppose you're working on **task 13**. You create a branch called **dev-task-13**, make changes, commit them, and then merge them back into **main** once the work is complete. This keeps your main branch stable.

### **Commit**
A **commit** captures the current state of the project, like a snapshot of all files. Each commit has:
- A unique identifier (`hash`).
- A descriptive message explaining the change.

### **Merge**
A **merge** combines changes from one branch into another, usually integrating a feature branch back into **main**.

### **Issues**
In GitHub, **issues** help track tasks, bugs, or feature requests, providing a structured way to manage development work.

## Repository Structure

### **HEAD**
`HEAD` is a pointer to the most recent commit in the current branch. When you make a new commit, `HEAD` updates to point to it.

### **Working Tree**
The **Working Tree** contains your project's files, where you modify and create content.

### **Index (Staging Area)**
The **index** is an intermediate storage area where Git tracks changes before committing.  
To add files to the index:
```shell
git add file.txt
```

## Main Commands

### `git commit`
Commits the staged changes, creating a new version in the repository.

**Commit Workflow:**
1. Check the status of modified files:
```bash
git status
```

2. Add files to the commit:
```bash
git add file1.txt file2.js

# or add all files

git add .
```

3. Create a commit with a message:
```bash
git commit -m "First Commit"
```
- The `-m` flag allows you to specify a message

### `git push`
Uploads local changes to the remote repository.

**Push Workflow:**
1. Push changes to the remote repository
```bash
git push
```

2. If this is the first push to a new remote branch:
```bash
git push -u origin main
```
- The `-u` flag sets up tracking for future pushes and pulls.

### `git pull`
Fetches and merges changes from the remote repository into the local branch.

**Pull Workflow:**
1. Get the latest updates:
```bash
git pull origin main
```

2. If tracking is already set up:
```bash
git pull
```

### `git tag`
A `tag` marks a specific commit in Git history, commonly used for versioning.

**Tag Workflow:**
1. List existing tags:
```bash
git tag
```

2. Create a new annotated tag:
```bash
git tag -a v1.0 -m "Version 1.0"
```
- `-a` creates an annotated tag.
- `v1.0` is the tag name.
- `-m` specifies a message.

3. Push the tag to the remote repository:
```bash
git push origin v1.0
```

### `git init`
Initializes a new Git repository in the current directory.
```bash
git init
```

### `git clone`
Creates a local copy of a remote repository.
```bash
git clone https://github.com/lorenzouriel/ebook-git-github.git
```

### **Architecture, Concepts and Commands:**
- ![architecture_git](content/imgs/02/architecture_git.jpg)

## Creating a Local and Remote Repo
1. Go to your GitHub and create a new repository:
- ![1](content/imgs/02/git_new_repo.jpg)

2. Navigate to the local directory where you want to create the repository
```shell
cd c:\path\vagrant
```

3. This command creates a file called `README.md` and inserts the text `#up-website-with-vagrant` into it. The `>>` is a redirection operator that appends the text to the end of the file, or creates the file if it doesn't exist.
```shell
echo "# up-website-with-vagrant" >> README.md
```

4. Initializes a new Git repository in the current directory.
```shell
git init
```

5. Adds the file `README.md` to the index. This prepares the file to be included in the next commit.
```shell
git add README.md
```

6. Adds all changes (if any)
```shell
git add .
```

7. Creates the first commit in the repository with a message. The `-m` allows you to add the commit message directly on the command line.
```shell
git commit -m "first commit"
```

8. Renames the repository's default branch to `main`. This command is used to update the main branch name to follow the latest naming practices, replacing the old master.
```shell
git branch -M main
```

9. Adds a remote repository named "`origin`". The term "`origin`" is a standard term used to refer to the main remote repository. The URL is the repository's address on GitHub.
```shell
git remote add origin https://github.com/lorenzouriel/up-website-with-vagrant.git
```

10. Pushes the local repository to the remote repository ("`origin`") on the main branch. The -u establishes a tracking relationship, automatically associating the local branch with the remote branch. This is useful for future git pull and git push without having to specify the branch.
```shell
git push -u origin main
```

We can check our remote repository:
- ![10](content/imgs/02/10.jpg)

## What is Versioning and Tags?

Have you ever worked with version releases?

Or with Tags in Git?

Tags are very important in our projects - with them we can identify at what point in time the main releases and versions occurred.

It is a way to organize and document your work.

But when you add tags, will you know the difference between each number?

I'll explain the difference in a simple and practical way:
- **Major:** These are changes that are incompatible with previous versions (Did you restructure everything? Add +1 - v2.0.0)
- **Minor:** These are important changes that are compatible with the previous version (Did you add a new feature? Add +1 v2.1.0)
- **Correction:** Errors and bugs that do not affect the version (Did you find a bug and fix it? Add +1 v2.1.1)
- **Build:** This is an internal control of Git and versioning, it is not necessarily visible when you specify the version.

**Example:**
- ![tags_versioning](content/imgs/02/tags_versioning.jpg)

## Introduction to Markdown
Markdown is a lightweight markup language used to format text in a simple and easy-to-read way.

Created by John Gruber and Aaron Swartz in 2004, its goal is to be readable in plain text while allowing automatic conversion to HTML. Markdown is widely used for creating documents, writing blog posts, and producing `README.md` in code repositories.

#### Headings:
- Headings are created using the `#` symbol. The number of `#` indicates the level of the heading.
```md
# Heading Level 1
## Heading Level 2
### Heading Level 3
```

#### Lists:
- Markdown supports both ordered and unordered lists. 
```md
- Item 1
- Item 2
- Subitem 2.1
- Subitem 2.2

1. First item
2. Second item
1. Subitem 2.1
2. Subitem 2.2
```

#### Links:
- To create links, use square brackets for the link text and parentheses for the URL.
```md
[Link to my website](https://www.example.com)
```

#### Images:
- Images are inserted similarly to links, but with an exclamation point `!` before them.
```md
![Project Logo](images/logo.jpg)
```

#### Emphasis (bold and italics):
- To create emphasis in text, you can use asterisks or underscores. 
```md
This is an **amazing project** that uses _modern technologies_.
```

#### Quotes:
- To create a quote, use the `>` symbol.
```md
> "Be the best version of yourself." - Einstein
```

#### Tables:
- Tables can be created using `|` to separate columns and `-` to create the header row.
```md
| Name | Role |
|------------|------------------|
| John | Developer |
| Mary | Designer |
```

#### Code:
- To include code blocks, use three backticks before and after the block. You can specify the programming language for syntax highlighting.
- ![md_code](content/imgs/02/md_code.jpg)

So far we understand what makes up Git and how to start your first project, let's delve deeper into what we've seen so far!