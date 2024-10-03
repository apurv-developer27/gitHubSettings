Here's a step-by-step guide to create muliple or separate SSH keys using the `Ed25519` algorithm for different GitHub accounts (personal and work) on a single Windows machine.

### Step 1: Open PowerShell or Git Bash

1. Press `Win + R`, type `powershell`, and hit Enter (or open Git Bash if installed and open git base).

### Step 2: Generate the First SSH Key (Personal Email)

1. Run the following command to generate the first SSH key for your **personal email**:

   ```bash
   ssh-keygen -t ed25519 -C "your_personal_email@example.com"
   ```

   - `-t ed25519` specifies the Ed25519 algorithm.
   - `-C` adds a comment (here, it's your personal email).

2. You'll be asked to save the key. To distinguish it, save it as `id_ed25519_personal`:

   ```bash
   Enter file in which to save the key (/c/Users/YourName/.ssh/id_ed25519): /c/Users/YourName/.ssh/id_ed25519_personal
   ```

3. You may set a passphrase for added security, or leave it empty for no passphrase.

### Step 3: Generate the Second SSH Key (Work Email)

1. Now, generate the SSH key for your **work email**:

   ```bash
   ssh-keygen -t ed25519 -C "your_work_email@example.com"
   ```

2. Save this one with a different name, for example `id_ed25519_work`:

   ```bash
   Enter file in which to save the key (/c/Users/YourName/.ssh/id_ed25519): /c/Users/YourName/.ssh/id_ed25519_work
   ```

3. Set a passphrase or leave it blank as per your preference.

### Step 4: Add SSH Keys to SSH Agent

You need to add the keys to the SSH agent so that the appropriate key can be used when connecting to different GitHub accounts.

1. Start the SSH agent:

   ```bash
   eval $(ssh-agent -s)
   ```

2. Add your personal key:

   ```bash
   ssh-add ~/.ssh/id_ed25519_personal
   ```

3. Add your work key:
   ```bash
   ssh-add ~/.ssh/id_ed25519_work
   ```

### Step 5: Create SSH Config File

To let your system know which key to use for which GitHub account, you'll create an SSH configuration file.

1. Open the SSH config file or create one if it doesn’t exist:

   ```bash
   notepad ~/.ssh/config
   ```

2. Add the following configuration to use the correct key for each account:

   ```bash
   # Personal GitHub account
   Host github-personal
     HostName github.com
     User git
     PreferredAuthentications publickey
     IdentityFile ~/.ssh/id_ed25519_personal

   # Work GitHub account
   Host github-work
     HostName github.com
     User git
     PreferredAuthentications publickey
     IdentityFile ~/.ssh/id_ed25519_work
   ```

3. Save and close the file.

### Step 6: Adding SSH Keys to GitHub Accounts

1. Copy the contents of your personal SSH public key:

   ```bash
   cat ~/.ssh/id_ed25519_personal.pub
   ```

   ```
    clip < ~/.ssh/id_ed25519.pub
    # Copies the contents of the id_ed25519.pub file to your clipboard

    or

    cat ~/.ssh/id_ed25519.pub | clip

    or

    For mac We can directly copy the content of the public key file in the clipboard.

     pbcopy < ~/.ssh/github-rahul-office.pub
     pbcopy < ~/.ssh/github-rahul-personal.pub

   ```

2. Go to your [GitHub SSH settings](https://github.com/settings/keys) and add this key to your personal account.

3. Repeat the same for your work account:
   ```bash
   cat ~/.ssh/id_ed25519_work.pub
   ```
   Add it to your work GitHub account.

---

### Step 7: Use Different SSH URLs for Different Accounts

Now, when cloning or pushing/pulling to repositories, you'll need to use different host aliases (e.g., `github-personal` or `github-work`) as specified in your SSH config.

1. For your **personal account**, clone using:

   ```bash
   git clone git@{account1_host_in_config}:account1_username/repository.git
   # Account 1 host name which you set in your config file

    [e.g.] git clone git@github.com-apurv-personal:apurv-personal/TestRepo.git

   ```

2. For your **work account**, clone using:
   ```bash
   git clone git@{account1_host_in_config}:account2_username/repository.git
   # Account 2 host name which you set in your config file
   ```

Now you can work with multiple GitHub accounts using different SSH keys on the same machine!

### Step 8 create a new repository on the command line

echo "# testing-repo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:apurv_personal/testing-repo.git
git push -u origin main

### or push an existing repository from the command line

git remote add origin git@github.com:apurv_personal/testing-repo.git
git branch -M main
git push -u origin main

## If any error comes then follow belows setps

It seems like the issue may still be related to SSH configuration or the repository setup. Let's go deeper into resolving this step by step.

### Troubleshooting Steps:

#### 1. **Double-Check Repository Existence**

First, confirm that the repository `git_settings` exists under your GitHub account (`apurv-personal`). Visit the following URL in your browser:

```
https://github.com/apurv-personal/git_settings
```

- If the repository exists, proceed with the next steps.
- If it doesn't, you'll need to create it or make sure you're pushing to the correct repository.

#### 2. **Verify GitHub Account**

Make sure you're logged into GitHub with the account `apurv_personal`, and this is the account that owns the `git_settings` repository.

#### 3. **Check GitHub Repository Access Rights**

Ensure that the SSH key you're using has access rights to the `apurv_personal` repository. You can check if the SSH key is properly configured by running:

```bash
ssh -T git@github.com
```

This should give you a message like:

```bash
Hi apurv_personal! You've successfully authenticated, but GitHub does not provide shell access.
```

If you receive an authentication failure, the issue is with the SSH key or account mismatch. You'll need to:

- Make sure the correct SSH key is added to **Settings > SSH and GPG keys** on GitHub.
- If you're using multiple SSH keys (for different accounts), make sure you're using the right key for `apurv_personal` (explained further below).

#### 4. **Correct SSH Config for Multiple Accounts**

If you have multiple GitHub accounts, you might need to configure your SSH settings more specifically to handle them properly. To do this, you can modify your `~/.ssh/config` file:

1. Open the `~/.ssh/config` file (create it if it doesn't exist):

   ```bash
   nano ~/.ssh/config
   ```

2. Add the following configuration for your `apurv_personal` GitHub account:

   ```bash
   Host github.com-apurv_personal
     HostName github.com
     User git
     IdentityFile ~/.ssh/id_rsa_apurv_personal
   ```

   Replace `~/.ssh/id_rsa_apurv_personal` with the path to your private SSH key associated with `apurv-personal`.

3. Now, update your Git remote URL to match the new SSH config:

   ```bash
   git remote set-url origin git@github.com-apurv_personal:apurv_personal/git_settings.git
   ```

#### 5. **Test SSH Again**

After making the changes, test your SSH connection again:

```bash
ssh -T git@github.com-apurv_personal
```

It should display a successful authentication message.

#### 6. **Re-attempt Push**

Finally, try pushing again:

```bash
git push origin main
```

#### 7. **Permissions Check**

If you're still facing issues, check if your SSH key is correctly assigned with push/pull access to the repository on GitHub:

- Go to **Settings > SSH and GPG keys** on GitHub.
- Make sure the key is associated with the `apurv_personal` account.
- Try removing the key and adding it back to ensure it's registered correctly.

---

Let me know how these steps go or if there are any specific errors at any stage!
