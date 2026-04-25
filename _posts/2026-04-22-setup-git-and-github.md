---
layout: post
title: "Git & GitHub SSH Setup"
date: 2026-04-22
tags: [python, github, ssh, setup]
---

## Configure git one more time
From time to time, I reset my dev systems and need to configure Git and GitHub once more.  
I'm sure there is an automated way, but I prefer doing it old school — going through my tech notes and setting everything up step by step.  
Sharing it here for future reference.

---

## GitHub SSH & Initial Project Setup

### 0. Configure Git identity
```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
git config --global --list  # verify
```

### 1. Generate SSH key
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Use a unique filename, e.g.:
```bash
~/.ssh/id_ed25519_github
```

### 2. Start SSH agent
```bash
eval "$(ssh-agent -s)"
```

### 3. Configure SSH
```bash
touch ~/.ssh/config
open ~/.ssh/config
```
If file does not already exist*
Add:
```bash
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519_github
```

### 4. Add key to agent
```bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519_github
```
This makes SSH login seamless and avoids repeated prompts while keeping the key secure (in a background process).

### 5. Copy public key
```bash
pbcopy < ~/.ssh/id_ed25519_github.pub
```

### 6. Add key to GitHub
Paste it in:  
Settings → SSH and GPG keys

### 7. Test connection
```bash
ssh -T git@github.com
```

---

## Security Note

When connecting for the first time, verify GitHub’s SSH fingerprint.

Only trust it if it matches the official value from GitHub documentation.

---

## Initialize and Push Project

```bash
git init
git add .
git commit -m "initial commit"
git remote add origin git@github.com:username/repo.git
git push -u origin main
```

---

## Note
Official recommended steps can be found on GitHub https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account
