# Getting Started in the Git & GitHub Universe
## What is Git?
Git is a **version control system** designed to track changes in software projects and coordinate the work of multiple people on them.

Developed by **Linus Torvalds in 2005**, Git stands out for its efficiency, flexibility, and ability to handle projects of any size.

It records changes to the source code, allows multiple development branches to exist simultaneously, and facilitates the merging of code from different contributors.

The main function of Git is to allow multiple people to work on the same code simultaneously, without causing conflicts or data loss.

**Main features of Git:**
- **Distributed:** Each developer has a complete copy of the repository's history.
- **Performance:** Designed to be fast and efficient, even with large amounts of data.
- **Security:** Ensures the integrity of the code and the changes made.
- **Flexibility:** Supports a variety of workflows and development processes.

## Git Installation and Initial Configuration
**Step 1: Git Installation**

To install Git, follow the steps below according to your operating system:

**Windows:**
- Download the Git installer from the official website: https://git-scm.com/.
- Run the installer and follow the on-screen instructions, keeping the default settings.

**macOS:**
- Open Terminal.
- Run the command: `brew install git`. (Requires Homebrew, which can be installed from https://brew.sh/).

**Linux:**
- Open Terminal.
- Run the appropriate command for your distribution:
- Debian/Ubuntu: `sudo apt-get install git`.

**Step 2: Git Initial Configuration**

After installing Git, you need to configure it. Use the following commands in the terminal to configure your username and email, which will be used in your commits:
```shell
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

You can check your settings with the command:
```shell
git config --list
```

## GitHub Installation and Initial Configuration
**GitHub is a source code hosting platform that uses Git for version control.** It allows you to collaborate on projects and share code with other developers.

**Step 1: Creating a GitHub account**
- Go to https://github.com/.
- Click "Sign up" and follow the steps to create a new account.

**Step 2: Setting up Git to use GitHub (Windows)**
- Launch Git Bash and generate an SSH key for secure authentication:
- In the terminal, run: `ssh-keygen -t rsa -C "youremail@example.com"`.
- Press Enter to accept the default file location.
- Enter a secure password (or leave it blank).

- Add the SSH key to your GitHub:
- Copy the public key that was generated.
- Go to GitHub Settings > "SSH and GPG keys".
- Click "New SSH key", paste the key and save.

The steps are the same for other operating systems, you will need to understand which commands and where they save the SSH keys that were generated.

**Step 3: Connecting to GitHub**
To clone a repository from GitHub, use the command:
```shell
git clone git@github.com:username/repository-name.git
```
---