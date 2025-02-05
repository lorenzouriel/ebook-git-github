# A Guide to Getting Started in the Git & GitHub Universe

Version control is essential for modern development, and Git is the most popular tool for managing code changes. Combined with GitHub, a powerful cloud-based repository hosting service, it enables collaboration, version tracking, and efficient project management.

## What is Git?
Git is a distributed version control system (DVCS) that helps developers track changes in their code, collaborate with teams, and maintain a history of modifications.

### Why Use Git?
- Version Control – Keep track of all changes in your project.
- Branching & Merging – Work on different features without interfering with the main code.
- Collaboration – Easily share and merge code with teams.
- Backup & History – Never lose code and revert to previous versions if needed.

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

## Authentication 
### Via SSH 
1. Generate an SSH Key:
```bash
ssh-keygen -t ed25519 -C "example@example.com"
```

2. Copy the public key:
```bash
cat ~/.ssh/id_ed25519.pub
```

3.  Add it to GitHub > Settings > SSH and GPG keys
4. Test authentication:
```bash
ssh -T git@github.com
```

If successful, you'll see:
```bash
Hi your-username! You've successfully authenticated.
```
