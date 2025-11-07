# Switching to Work Account: Cursor + GitHub

## Current Status
- **Repository**: `regan178/gtm-map` (personal account)
- **GitHub Auth**: Using Cursor integration token
- **Git User**: Set to Cursor Agent (generic)

## Goal
Switch both **Cursor** and **GitHub** authentication to your **work account**.

---

## Step 1: Verify Your Cursor Account

1. **Check current Cursor account:**
   - In Cursor Mobile UI, look at your profile/avatar (top-right)
   - Or go to: **Settings → Account** (or **Preferences → Account**)
   - Note which email/account is currently logged in

2. **If you need to switch Cursor account:**
   - Sign out of current account
   - Sign in with your **work email/credentials**
   - Restart Cursor if prompted

---

## Step 2: Switch GitHub Authentication to Work Account

You have **two options**:

### Option A: Use GitHub CLI (Recommended)

1. **Log out of current GitHub CLI session:**
   ```bash
   gh auth logout
   ```

2. **Log in with your work account:**
   ```bash
   gh auth login
   ```
   - Select: **GitHub.com**
   - Choose: **HTTPS** (recommended)
   - Authenticate via: **Browser** (easiest)
   - When browser opens, make sure you're logged into your **work GitHub account**
   - Authorize GitHub CLI

3. **Configure Git to use GitHub CLI:**
   ```bash
   gh auth setup-git
   ```

4. **Verify you're on the right account:**
   ```bash
   gh api user --jq '.login'
   ```
   Should show your **work GitHub username**

### Option B: Use Personal Access Token (PAT)

1. **Generate a Personal Access Token for your work account:**
   - Go to: https://github.com/settings/tokens (make sure you're logged into **work account**)
   - Click: **Generate new token** → **Generate new token (classic)**
   - Name it: "Cursor Work Account"
   - Select scopes:
     - ✅ `repo` (Full control of private repositories)
     - ✅ `workflow` (if you use GitHub Actions)
   - Click **Generate token**
   - **Copy the token immediately** (you won't see it again!)

2. **Update Git remote with your work account:**
   ```bash
   # Replace WORK_USERNAME with your work GitHub username
   # Replace YOUR_TOKEN with the token you just generated
   git remote set-url origin https://WORK_USERNAME:YOUR_TOKEN@github.com/WORK_USERNAME/gtm-map.git
   ```

   Or if the repo should stay under a different account:
   ```bash
   git remote set-url origin https://YOUR_TOKEN@github.com/regan178/gtm-map.git
   ```

3. **Update Git user config:**
   ```bash
   git config --global user.name "Your Work Name"
   git config --global user.email "your.work.email@company.com"
   ```

---

## Step 3: Verify Everything is Connected

Run these commands to verify:

```bash
# Check GitHub CLI account
gh api user --jq '.login'

# Check Git remote
git remote -v

# Check Git user config
git config --global user.name
git config --global user.email

# Test authentication (should not prompt for credentials)
git fetch origin
```

---

## Step 4: Update Repository Remote (If Needed)

If your work account has its own copy of the repository, or you need to change the remote:

```bash
# Update to work account's repository
git remote set-url origin https://github.com/WORK_USERNAME/gtm-map.git

# Or if using SSH
git remote set-url origin git@github.com:WORK_USERNAME/gtm-map.git
```

---

## Important Notes

1. **Cursor Account**: The Cursor account determines which agents and features you have access to. Make sure you're signed into your **work Cursor account**.

2. **GitHub Account**: The GitHub account determines which repositories you can access and push to. These are **separate** authentications.

3. **Both Need to Match**: For agents to work with your work repositories, you need:
   - ✅ Cursor signed into **work account**
   - ✅ GitHub authenticated as **work account**

4. **Repository Ownership**: The repository `regan178/gtm-map` appears to be under a personal account. You may need to:
   - Transfer it to your work account, OR
   - Create a new repository under your work account, OR
   - Keep using the personal account's repo but authenticate with work account (if you have access)

---

## Quick Checklist

- [ ] Cursor signed into work account (check Settings → Account)
- [ ] GitHub CLI authenticated with work account (`gh auth login` with work account)
- [ ] Git user config set to work name/email
- [ ] Git remote updated (if repository moved to work account)
- [ ] Test push/pull works without errors

---

## Troubleshooting

**"Permission denied" when pushing:**
- Verify GitHub token has `repo` scope
- Check you're authenticated with the correct account
- Ensure you have write access to the repository

**Cursor agents not working:**
- Verify Cursor is signed into work account
- Restart Cursor after switching accounts
- Check Cursor account has agent access enabled

**GitHub CLI shows wrong account:**
- Run `gh auth logout` then `gh auth login` again
- Make sure browser opens with work account logged in
