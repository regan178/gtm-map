# Fixing GitHub Push Permissions in Cursor

## The Problem
Cursor is asking to create a fork because it doesn't have write permissions to your repository. This is an authentication issue.

## Solution: Authenticate Cursor with GitHub

### Method 1: Use GitHub Personal Access Token (Recommended)

1. **Generate a Personal Access Token on GitHub:**
   - Go to: https://github.com/settings/tokens
   - Click "Generate new token" → "Generate new token (classic)"
   - Name it: "Cursor Editor" or similar
   - Select scopes:
     - ✅ `repo` (Full control of private repositories)
     - ✅ `workflow` (if you use GitHub Actions)
   - Click "Generate token"
   - **Copy the token immediately** (you won't see it again!)

2. **Configure Git to use the token:**
   ```bash
   git config --global credential.helper wincred
   ```

3. **Update your remote URL to include your username:**
   ```bash
   git remote set-url origin https://regan178@github.com/regan178/gtm-map.git
   ```

4. **Try pushing again:**
   - When prompted for password, paste your **Personal Access Token** (not your GitHub password)

### Method 2: Use SSH Instead of HTTPS (More Secure)

1. **Check if you have SSH keys:**
   ```bash
   ls ~/.ssh/id_*.pub
   ```

2. **If no SSH key exists, generate one:**
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   - Press Enter to accept default location
   - Optionally set a passphrase

3. **Add SSH key to GitHub:**
   - Copy your public key:
     ```bash
     cat ~/.ssh/id_ed25519.pub
     ```
   - Go to: https://github.com/settings/keys
   - Click "New SSH key"
   - Paste the key and save

4. **Switch remote to SSH:**
   ```bash
   git remote set-url origin git@github.com:regan178/gtm-map.git
   ```

5. **Test connection:**
   ```bash
   ssh -T git@github.com
   ```

### Method 3: Use GitHub CLI (gh)

1. **Install GitHub CLI** (if not installed):
   - Download from: https://cli.github.com/

2. **Authenticate:**
   ```bash
   gh auth login
   ```
   - Follow the prompts
   - Select "GitHub.com"
   - Choose authentication method (browser recommended)

3. **Configure Git to use gh:**
   ```bash
   gh auth setup-git
   ```

## Verify Authentication

After setting up, test with:
```bash
git push origin main
```

If it still asks for a fork, the authentication isn't working yet.

## Quick Fix for Right Now

If you need to push immediately:

1. **Use command line with token:**
   ```bash
   git remote set-url origin https://YOUR_TOKEN@github.com/regan178/gtm-map.git
   ```
   (Replace YOUR_TOKEN with your Personal Access Token)

2. **Or use GitHub Desktop:**
   - Download GitHub Desktop
   - It handles authentication automatically
   - Push from there

## Common Issues

**"Permission denied" after setting up:**
- Make sure your token has `repo` scope
- Check that you're using the correct username (`regan178`)

**"Repository not found":**
- Verify the repo exists at: https://github.com/regan178/gtm-map
- Check you're logged into the correct GitHub account

**Cursor still asking for fork:**
- Restart Cursor after authentication changes
- Check Cursor's GitHub extension settings
- Try Method 2 (SSH) for more reliable authentication

## Recommended: SSH Method

SSH is more secure and doesn't require tokens that expire. Once set up, it "just works" without password prompts.

