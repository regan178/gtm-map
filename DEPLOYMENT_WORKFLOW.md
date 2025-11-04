# Deployment Workflow: Cursor → GitHub → Vercel

## Overview

Your Vercel project is connected to your GitHub repository (`regan178/gtm-map`). When you push changes to the `main` branch on GitHub, Vercel automatically detects the changes and redeploys your site.

## Two Workflow Options

### Option 1: Direct Push to Main (Simplest)
**Best for**: Quick updates, solo projects, small changes

1. Make changes in Cursor
2. Use GitHub Pull Request extension to:
   - Stage changes
   - Commit with a message
   - Push directly to `main` branch
3. Vercel auto-deploys (1-3 minutes)

### Option 2: Pull Request Workflow (Recommended)
**Best for**: Code review, collaboration, preview deployments

1. **Create a new branch** (using GitHub PR extension):
   - Branch name: `feature/your-feature-name` or `update/description`
   
2. **Make your changes** in Cursor

3. **Commit and push the branch** (using GitHub PR extension):
   - Stage changes
   - Commit with descriptive message
   - Push the branch (not main)

4. **Create Pull Request** (using GitHub PR extension):
   - The extension will let you create a PR
   - Vercel creates a **preview deployment** for the PR
   - Review your changes

5. **Merge the PR**:
   - Merge to `main` branch
   - Vercel auto-deploys to production

## Using GitHub Pull Request Extension in Cursor

### Creating a Pull Request Workflow:

1. **Create Branch**:
   - Open Source Control panel (Ctrl+Shift+G)
   - Click "..." menu → "Branch" → "Create Branch"
   - Name it (e.g., `update-companies-list`)

2. **Make Changes**:
   - Edit your files normally

3. **Stage & Commit**:
   - Click "+" next to changed files to stage
   - Enter commit message
   - Click "Commit" button

4. **Push Branch**:
   - Extension will prompt to push
   - Or use "..." → "Push" → "Push to..."

5. **Create Pull Request**:
   - Extension should show "Create Pull Request" option
   - Or go to GitHub website and create PR there
   - Vercel will create a preview deployment automatically

6. **Merge PR**:
   - Review changes in preview
   - Merge PR on GitHub
   - Vercel deploys to production

## Current Status

✅ **GitHub Repository**: Connected (`regan178/gtm-map`)  
✅ **Vercel Integration**: Connected to `main` branch  
⚠️ **Action Needed**: You have 1 local commit that needs to be pushed

**To push your current commit using the extension:**
- Open Source Control panel
- Click "..." → "Push" → "Push to..."
- Select `origin/main`

Or create a PR:
- Create a branch from your current commit
- Push the branch
- Create PR via extension
- Merge when ready

## Quick Reference

**Check status:**
- Source Control panel shows uncommitted/unpushed changes

**See branches:**
- Bottom left status bar shows current branch
- Click to switch/create branches

**Create PR:**
- Push branch → Extension prompts for PR creation
- Or visit: `https://github.com/regan178/gtm-map/pulls`

**View Vercel deployments:**
- Production: Auto-deploys when PR merges to `main`
- Preview: Created for each PR automatically
- Visit: https://vercel.com/dashboard → `gtm-map` project

## Troubleshooting

### Extension not showing PR option:
- Make sure you've pushed the branch first
- Check that you're authenticated with GitHub in Cursor
- Try creating PR directly on GitHub website

### Vercel preview not showing:
- Check PR has been created on GitHub
- Look in Vercel dashboard under "Deployments"
- Preview URLs appear as comments on the PR

### Merge conflicts:
- Extension will show conflicts
- Resolve in Cursor or on GitHub
- Then merge the PR

## Pro Tips

1. **Use PRs for review**: Even solo, PRs give you preview deployments
2. **Descriptive branch names**: `update-companies`, `fix-logo-loading`, etc.
3. **Check previews**: Vercel creates preview URLs for each PR
4. **Small PRs**: Easier to review and deploy safely

## What Happens Behind the Scenes

**Direct Push:**
1. Push to `main` → GitHub webhook → Vercel detects → Builds → Deploys

**PR Workflow:**
1. Push branch → Create PR → Vercel creates preview deployment
2. Merge PR → Vercel deploys to production
3. Both preview and production URLs available

---

**The GitHub PR extension makes this workflow seamless!** Use it to create branches, commit, push, and create PRs all from within Cursor.
