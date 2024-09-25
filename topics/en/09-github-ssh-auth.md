# GitHub Authentications
GitHub no longer supports password authentication for HTTPS Git operations as of August 13, 2021. If you tried to connect, you probably received an error.

To resolve this, you need to use one of the currently supported authentication methods. The most common way is to use a personal access token (PAT) or use an SSH key.

## SSH

### 1. Check for Existing SSH Keys
Before generating a new SSH key, check if you already have one on your syste
``` bash
ls -al ~/.ssh
```

If you see files like `id_rsa` and `id_rsa.pub`, you already have an SSH key pair. If not, proceed to generate a new one.

### 2. Generate a New SSH Key
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

### 3. Save the SSH Key
When prompted to "Enter a file in which to save the key," press Enter to accept the default location `(~/.ssh/id_ed25519 or ~/.ssh/id_rsa)`.

You'll then be asked to enter a passphrase. You can either:
- Enter a secure passphrase (recommended for better security), or
- Press Enter to skip creating a passphrase (less secure but more convenient).

### 4. Add Your SSH Key to the SSH Agent
To manage your SSH key, you need to ensure the SSH agent is running:
```bash
eval "$(ssh-agent -s)"
```

Now, add your SSH private key to the agent:
```bash
ssh-add ~/.ssh/id_ed25519
```
- *(Or `~/.ssh/id_rsa` if you used RSA.)*

### 5. Add the SSH Key to GitHub
Now you need to add the public key to GitHub:
- Display the public key:
```bash
cat ~/.ssh/id_ed25519.pub
```
- Copy the output (this is your public key).
- Go to GitHub [SSH and GPG Keys](https://github.com/settings/keys).
- Click New SSH key, provide a title (e.g., "My Machine SSH"), and paste your public key into the "Key" field.
- Click Add SSH key.

### 6. Test Your SSH Connection
Test if the SSH key is working by running:
```bash
ssh -T git@github.com
```

If it's successful, you'll see a message like:
```bash
Hi lorenzouriel! You've successfully authenticated, but GitHub does not provide shell access.
```

### 7. Change Your Git Remote URL to Use SSH
Now update your Git remote to use SSH:
```bash
git remote set-url origin git@github.com:lorenzouriel/ebook-git-github.git
```

### 8. Push Your Changes
Now try pushing your changes:
```bash
git push -u origin main
```

This should work without asking for your username or password!