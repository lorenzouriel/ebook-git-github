# A Guide to Getting Started in the Git & GitHub
Who are they? Where do they live? What do they eat? And, best of all, how to install it?

## What is Git?
Git is a **version control system** designed to track changes in software projects and coordinate the work of multiple people on them.

Developed by **Linus Torvalds in 2005**, Git stands out for its efficiency, flexibility, and ability to handle projects of any size.

It records changes to the source code, allows multiple development branches to exist simultaneously, and facilitates the merging of code from different contributors.

The main function of Git is to allow multiple people to work on the same code simultaneously, without causing conflicts or data loss.

## Git Installation and Initial Configuration
### Installing Git
#### Windows
1. Download Git from: https://git-scm.com/downloads
2. Run the installer and select default options
3. Open Git Bash and verify installation:
```bash
git --version
```

#### macOS:
1. Install Git via Homebrew:
```bash
brew install git
```

2. Verify installation:
```bash
git --version
```

#### Linux (Debian-based):
```bash
sudo apt update && sudo apt install git
git --version
```

### Initial Git Configuration
After installing Git, configure your identity:
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Check your settings with:
```bash
git config --list
```

These settings ensure your commits are properly attributed.

## What is GitHub?

GitHub is a platform for version control and collaboration using Git. It allows multiple developers to work on the same project, track changes, and manage code repositories efficiently.  

With GitHub, you can:  
- Host and share repositories  
- Collaborate with teams using pull requests and code reviews  
- Automate workflows with GitHub Actions  
- Manage project tasks with Issues and Projects   

## GitHub Authentications
GitHub no longer supports password authentication for HTTPS Git operations since August 2021. If you tried to connect, you probably received an error.

To resolve this, you need to use one of the currently supported authentication methods. The most common way is to use a personal access token (PAT) or use an SSH key.

### SSH

#### 1. Check for Existing SSH Keys
Before generating a new SSH key, check if you already have one on your system
``` bash
ls -al ~/.ssh
```

If you see files like `id_rsa` and `id_rsa.pub`, you already have an SSH key pair. If not, proceed to generate a new one.

#### 2. Generate a New SSH Key
To generate a new SSH key pair, run the following command:
```bash
ssh-keygen -t ed25519 -C "your_email@gmail.com"
```
- *Replace `your_email@gmail.com` with the email you use for GitHub.*

If your system doesn't support the `ed25519` algorithm, use `rsa`:
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@gmail.com"
```
- *Replace `your_email@gmail.com` with the email you use for GitHub.*

This command creates a new SSH key using the provided email as a label.

#### 3. Save the SSH Key
When prompted to "Enter a file in which to save the key," press Enter to accept the default location `(~/.ssh/id_ed25519 or ~/.ssh/id_rsa)`.

You'll then be asked to enter a passphrase. You can either:
- Enter a secure passphrase (recommended for better security)
- Press Enter to skip creating a passphrase (less secure but more convenient)

#### 4. Add Your SSH Key to the SSH Agent
To manage your SSH key, you need to ensure the SSH agent is running:
```bash
eval "$(ssh-agent -s)"
```

Now, add your SSH private key to the agent:
```bash
ssh-add ~/.ssh/id_ed25519
```
- *(Or `~/.ssh/id_rsa` if you used RSA.)*

#### 5. Add the SSH Key to GitHub
Now you need to add the public key to GitHub:
- Display the public key:
```bash
cat ~/.ssh/id_ed25519.pub
```
- Copy the output (this is your public key).
- Go to GitHub [SSH and GPG Keys](https://github.com/settings/keys).
- Click New SSH key, provide a title (e.g., "My Machine SSH"), and paste your public key into the "Key" field.
- Click Add SSH key.

#### 6. Test Your SSH Connection
Test if the SSH key is working by running:
```bash
ssh -T git@github.com
```

If it's successful, you'll see a message like:
```bash
Hi lorenzouriel! You've successfully authenticated, but GitHub does not provide shell access.
```

#### 7. Change Your Git Remote URL to Use SSH
Now update your Git remote to use SSH:
```bash
git remote set-url origin git@github.com:lorenzouriel/ebook-git-github.git
```

#### 8. Push Your Changes
Now try pushing your changes:
```bash
git push -u origin main
```

This should work without asking for your username or password.

Now you can start working with Git & GitHub!