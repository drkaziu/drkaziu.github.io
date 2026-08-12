---
layout: post
title: "Configure Git and GitHub on macOS"
date: 2026-04-22
tags: [git, github, ssh, macos, setup]
---

From time to time, I reset my development system and need to configure Git and GitHub again.

There are automated ways to do this, but I prefer going through my notes and setting everything up step by step. I am sharing the process here for future reference.

## Configure Git identity

Your Git name and email are included in every commit and may be visible in public repositories. For additional privacy, use the GitHub provided `noreply` email shown under **GitHub → Settings → Emails**.

```bash
git config --global user.name "Your Name"
git config --global user.email "YOUR_ID+USERNAME@users.noreply.github.com"
git config --global init.defaultBranch main
```

Verify the configuration:

```bash
git config --global --list
```

Authentication credentials are separate from this identity. Your SSH private key remains on your Mac and should never be shared or committed.

## Generate an SSH key

```bash
ssh-keygen -t ed25519 -C "YOUR_ID+USERNAME@users.noreply.github.com"
```

When prompted for a location, use a descriptive filename:

```text
~/.ssh/id_ed25519_github
```

Set a strong passphrase. macOS Keychain can remember it, so you will not need to enter it for every connection.

## Start the SSH agent

```bash
eval "$(ssh-agent -s)"
```

## Configure SSH

Create the SSH directory and configuration file if they do not exist:

```bash
mkdir -p ~/.ssh
touch ~/.ssh/config
open -e ~/.ssh/config
```

Add the following configuration:

```sshconfig
Host github.com
  HostName github.com
  User git
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519_github
  IdentitiesOnly yes
```

Set appropriate permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/config
chmod 600 ~/.ssh/id_ed25519_github
chmod 644 ~/.ssh/id_ed25519_github.pub
```

## Add the private key to macOS Keychain

```bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519_github
```

This allows the SSH agent to use the key while macOS Keychain securely remembers its passphrase.

## Add the public key to GitHub

Copy the public key:

```bash
pbcopy < ~/.ssh/id_ed25519_github.pub
```

Open **GitHub → Settings → SSH and GPG keys → New SSH key**. Choose **Authentication Key**, paste the public key, give it a recognizable name such as `MacBook Pro`, and save it.

The `.pub` file can be shared safely. The private key without the `.pub` extension must remain secret.

## Test the connection

```bash
ssh -T git@github.com
```

A successful connection should return a message similar to:

```text
Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

The first connection may ask you to confirm GitHub's host fingerprint. Compare it with the fingerprints in the [official GitHub documentation](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints) before accepting it.

## Initialize and push a project

First, create an empty repository on GitHub. If the local project already contains files, do not initialize the GitHub repository with a README, license, or `.gitignore`.

Before staging files, create an appropriate `.gitignore` and make sure the project does not contain passwords, API keys, tokens, `.env` files, private datasets, or other sensitive information.

From the local project directory, run:

```bash
git init -b main
git status
git add .
git diff --cached
git commit -m "Initial commit"
git remote add origin git@github.com:USERNAME/REPOSITORY.git
git remote -v
git push -u origin main
```

Reviewing `git status` and `git diff --cached` before committing helps prevent accidental publication of unwanted or sensitive files.

## Official documentation

- [Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
