# Fundamental Concepts
## Introduction to Repositories and Concepts
A repository is the place where the project, its changes and files are stored. It can be local or remote, each with its own specific characteristics:
- **Remote:** Hosted on platforms such as GitHub, other version control systems (CVS) or dedicated servers.
- **Local:** Stored directly on the developer's machine.

### **Main Concepts**
#### Branches
**Branches (or branches) are parallel versions of the project.** The main branch is usually called **main**, but it is possible to create new branches to develop specific changes without affecting the main branch.
- **Example:** Create a branch called **dev-task-13**, in this branch you will focus on finishing task 13 of your backlog, when you finish you **commit** and do a **merge** with the main branch. This way, you do not affect your main branch with changes that could break the code.

#### Commit
A commit is an operation that captures the current state of the project. It's like taking a snapshot of the files at that moment. Each commit has a unique identifier (`hash`) and a descriptive message.

#### Merge
A merge is the operation of combining changes from different branches. Typically, you perform a merge when you want to integrate changes from a feature or bug fix branch back into the main branch.

#### Issues
In the context of Git, an issue refers to a way to track tasks, enhancements, bugs, or discussions related to a specific project.

### **Repository Structure**
#### HEAD
The `HEAD` is a pointer that points to the **most recent commit in the current branch**. When you make a new commit, the `HEAD` moves to that new commit. It is also used to determine the current state of the Working Tree and the Index.

#### Working Tree
The Working Tree is where the files are actually stored and where you make your changes.

#### Index
The index is where Git stores what will be committed. It acts as an intermediate area between the Working Tree and the Git repository. To add files to the index, we use the command: `git add file.txt`

### **Git Architecture and Concepts**
- ![architecture_git](/topics/imgs/02/architecture_git.jpg)

## Main Commands
### **`Commit`**
This happens when we want to save the latest updates that were made.

**Processes related to Commit:**
- Check the status of the modified files:
```shell
git status
```

- Add the files to the commit:

```shell
git add file1.txt file2.js

git add .
```

- Perform the commit:
```shell
git commit -m "First Commit"
```

The `-m` is used to add a message to the commit, followed by the text `"First Commit"`.

### **`Push`**
This happens when we send the changes to the repository - it "pushes" the modifications to the remote repository

**Processes related to Push:**
- Perform the push to the remote repository:
```shell
git push

# or

git push origin branch-name
```

- If this is the first connection and first push:
```shell
git push -u origin branch-name
```

You need to configure the relationship between the local and remote branches using the command above.

The `-u` establishes a tracking relationship, facilitating future pushes and pulls.

### **`Pull`**
Updates your local repository with the changes in the remote repository - "pulls" the changes from the remote repository.

It brings all the changes from your remote repository to your local repository.

**Pull-related processes:**
- Perform a pull to get the latest changes:
```shell
git pull origin branch-name
```

- If you have already set up the tracking relationship during git push `-u`, you can just use:
```shell
git pull
```

### **`Tag`**
A tag in Git is a specific reference to a point in the history of your repository. It is commonly used to mark stable or important versions of your project.

Tags are useful for creating fixed reference points that do not move as new commits are made.

**Tag-related processes:**
- List existing tags:
```shell
git tag
```

- Create a new tag:
```shell
git tag -a v1.0 -m "Version 1.0"
```
- This command creates an annotated tag named `"v1.0"` with a descriptive message `"Version 1.0"`.
- **1. a: Creates an annotated tag.**
- **2. v1.0: Tag name.**
- **3. -m "Version 1.0": Descriptive message associated with the tag.**

- Share the tag to the remote repository:
```shell
git push origin v1.0
```

### **`init`**
Initializes a new Git repository in the current directory.
```shell
git init
```

### **`clone`**
Clones a remote repository to your computer. 
```shell
git clone <repository-url>
```

## Creating a Local and Remote Repo
**1. Go to your GitHub and create a new repository:**
- ![1](/topics/imgs/02/1.png)

**2. Navigate to the local directory where you want to create the repository — use the cd p command to enter the desired directory.**
```shell
cd c:\path\vagrant
```

**3. This command creates a file called README.md and inserts the text #up-website-with-vagrant into it. The >> is a redirection operator that appends the text to the end of the file, or creates the file if it doesn't exist.**
```shell
echo "# up-website-with-vagrant" >> README.md
```

**4. Initializes a new Git repository in the current directory.**
```shell
git init
```

**5. Adds the file README.md to the index. This prepares the file to be included in the next commit.**
```shell
git add README.md
```

**6. Adds all changes (if any)**
```shell
git add .
```

**7. Creates the first commit in the repository with a message. The -m allows you to add the commit message directly on the command line.**
```shell
git commit -m "first commit"
```

**8. Renames the repository's default branch to main. This command is used to update the main branch name to follow the latest naming practices, replacing the old master**
```shell
git branch -M main
```

**9. Adds a remote repository named "origin". The term "origin" is a standard term used to refer to the main remote repository. The URL is the repository's address on GitHub.**
```shell
git remote add origin https://github.com/lorenzouriel/up-website-with-vagrant.git
```

**10. Pushes the local repository to the remote repository ("origin") on the main branch. The -u establishes a tracking relationship, automatically associating the local branch with the remote branch. This is useful for future git pull and git push without having to specify the branch.**
```shell
git push -u origin main
```

We can check our remote repository:
- ![10](/topics/imgs/02/10.png)

### What is Versioning and Tags?

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
- ![tags_versioning](/topics/imgs/02/tags_versioning.png)

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
- Markdown supports both ordered and unordered lists. ```md
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
``md
![Project Logo](images/logo.png)
```

#### Emphasis (bold and italics):
- To create emphasis in text, you can use asterisks or underscores. ```md
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
- ![md_code](/topics/imgs/02/md_code.png)
---