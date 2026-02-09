# FCS Commercial V2 - Complete Deployment Guide

**Date Created:** February 8, 2026
**Purpose:** Step-by-step guide to recreate this deployment process for future versions

---

## 📋 Table of Contents

1. [Prerequisites](#prerequisites)
2. [Initial Repository Setup](#initial-repository-setup)
3. [File Preparation](#file-preparation)
4. [GitHub Pages Configuration](#github-pages-configuration)
5. [Updating Content](#updating-content)
6. [Troubleshooting](#troubleshooting)
7. [Complete Command Reference](#complete-command-reference)

---

## Prerequisites

### Required Tools
- Git Bash (Windows) or Terminal (Mac/Linux)
- GitHub CLI (`gh`) installed and authenticated
- Git configured with your credentials
- Access to SyncShepherd-Main GitHub organization

### Check Prerequisites
```bash
# Verify Git is installed
git --version

# Verify GitHub CLI is installed
gh --version

# Verify GitHub CLI is authenticated
gh auth status
```

---

## Initial Repository Setup

### Step 1: Create GitHub Repository

```bash
# Create a new public repository
gh repo create SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2 --public

# Expected output:
# ✓ Created repository SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2 on GitHub
```

**Important Notes:**
- Repository must be public for GitHub Pages to work on free tier
- Use descriptive naming: `Claude_FCS_Commercial_Mockup_V2`, `V3`, etc.
- Organization: `SyncShepherd-Main`

---

## File Preparation

### Step 2: Create Local Working Directory

```bash
# Navigate to your working directory
cd /e/Downloads

# Create a new directory for the project
mkdir fcs-commercial-v2
cd fcs-commercial-v2
```

### Step 3: Extract and Organize Files

**If you have a ZIP file:**
```bash
# Extract the ZIP file
unzip /path/to/fcs-commercial-github_v5.zip -d /e/Downloads/fcs-commercial-v5

# Copy files to your working directory
cp -r /e/Downloads/fcs-commercial-v5/* /e/Downloads/fcs-commercial-v2/
```

**Expected File Structure:**
```
fcs-commercial-v2/
├── index.html (root redirect)
├── .nojekyll (for GitHub Pages)
├── commercial-services/
│   └── index.html (hub page)
├── commercial-foundation-repair/
│   └── index.html
├── commercial-concrete-services/
│   └── index.html
├── commercial-drainage-solutions/
│   └── index.html
├── commercial-retaining-walls/
│   └── index.html
├── commercial-excavation/
│   └── index.html
├── commercial-mudjacking/
│   └── index.html
├── commercial-multi-family/
│   └── index.html
├── commercial-office-corporate/
│   └── index.html
├── commercial-industrial/
│   └── index.html
├── commercial-medical-offices/
│   └── index.html
└── commercial-home-builders/
    └── index.html
```

### Step 4: Create .nojekyll File

**This is CRITICAL for GitHub Pages to work correctly!**

```bash
cd /e/Downloads/fcs-commercial-v2
touch .nojekyll
```

**Why .nojekyll is important:**
- GitHub Pages uses Jekyll by default
- Jekyll ignores directories starting with underscore or certain patterns
- `.nojekyll` tells GitHub Pages to skip Jekyll processing
- Without it, your site may not deploy correctly

---

## Initial Git Setup and Push

### Step 5: Initialize Git Repository

```bash
cd /e/Downloads/fcs-commercial-v2

# Initialize git
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: FCS Commercial Website V2

- 13 HTML pages (1 hub + 12 service/sector pages)
- Clean directory structure
- Inline CSS for portability
- Mobile-responsive design
- Schema.org markup
- .nojekyll for GitHub Pages compatibility"

# Add remote origin
git remote add origin https://github.com/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2.git

# Push to GitHub
git push -u origin main
```

**Expected Output:**
```
Enumerating objects: X, done.
Counting objects: 100% (X/X), done.
Delta compression using up to N threads
Compressing objects: 100% (X/X), done.
Writing objects: 100% (X/X), XXX KiB | XXX MiB/s, done.
Total X (delta X), reused 0 (delta 0), pack-reused 0
To https://github.com/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

---

## GitHub Pages Configuration

### Step 6: Enable GitHub Pages via API

**Important:** Use `MSYS_NO_PATHCONV=1` on Git Bash to prevent path rewriting issues.

```bash
# Enable GitHub Pages (Git Bash on Windows)
MSYS_NO_PATHCONV=1 gh api -X POST repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages \
  -f source[branch]=main \
  -f source[path]=/
```

**For Mac/Linux:**
```bash
# Enable GitHub Pages (Mac/Linux)
gh api -X POST repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages \
  -f source[branch]=main \
  -f source[path]=/
```

**Expected Response:**
```json
{
  "url": "https://api.github.com/repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages",
  "status": "built",
  "html_url": "https://syncshepherd-main.github.io/Claude_FCS_Commercial_Mockup_V2/",
  "source": {
    "branch": "main",
    "path": "/"
  },
  "public": true,
  "https_enforced": true
}
```

### Step 7: Verify GitHub Pages Status

```bash
# Check GitHub Pages status
MSYS_NO_PATHCONV=1 gh api repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages
```

**Look for:**
- `"status": "built"` ✅
- `"html_url"` with your live site URL
- `"https_enforced": true` ✅

### Step 8: Check Build Status

```bash
# Check latest build
MSYS_NO_PATHCONV=1 gh api repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages/builds/latest
```

**Success indicators:**
- `"status": "built"`
- No errors in `"error"` field
- Recent `"updated_at"` timestamp

---

## Updating Content

### Scenario 1: Replace All Files with New Version

```bash
cd /e/Downloads/fcs-commercial-v2

# Remove all existing files (except .git)
git rm -rf .
git clean -fdx

# Copy new files
cp -r /path/to/new-version/* .

# Ensure .nojekyll exists
touch .nojekyll

# Add all files
git add .

# Commit with descriptive message
git commit -m "Replace with v5 site structure

- 13 pages with clean directory structure
- Updated content for all service pages
- Improved mobile responsiveness"

# Force push to replace everything
git push -f origin main
```

**⚠️ Warning:** Force push (`-f`) overwrites remote history. Use carefully!

### Scenario 2: Update Individual Files

```bash
cd /e/Downloads/fcs-commercial-v2

# Edit files as needed
# (use text editor or copy updated files)

# Check what changed
git status

# Add specific files
git add commercial-services/index.html
git add commercial-foundation-repair/index.html

# Or add all changes
git add .

# Commit with descriptive message
git commit -m "Update hub page and foundation repair content

- Added new testimonials
- Updated pricing information
- Improved FAQ section"

# Push to GitHub
git push origin main
```

### Scenario 3: Add New Pages

```bash
cd /e/Downloads/fcs-commercial-v2

# Create new directory
mkdir commercial-new-service

# Create index.html in new directory
# (copy from existing page and modify)

# Add to git
git add commercial-new-service/

# Commit
git commit -m "Add new service page: Commercial New Service

- Created new service directory
- Added comprehensive content
- Updated navigation links"

# Push
git push origin main
```

---

## Creating README

### Step 9: Create README.md

```bash
cd /e/Downloads/fcs-commercial-v2

# Create README (use text editor or copy template)
# See README.md in this repository for template

# Add README
git add README.md

# Commit
git commit -m "Add comprehensive README with site structure and live demo links"

# Push
git push origin main
```

**README should include:**
- Live demo link with badge
- Project overview
- Site structure table
- Technical details
- Deployment instructions
- Version history

---

## Troubleshooting

### Issue 1: Site Not Displaying (404 Error)

**Symptoms:**
- Visiting site URL shows 404 error
- GitHub says Pages is enabled

**Solutions:**

1. **Check .nojekyll file exists:**
   ```bash
   cd /e/Downloads/fcs-commercial-v2
   ls -la | grep nojekyll
   ```
   If missing, create it:
   ```bash
   touch .nojekyll
   git add .nojekyll
   git commit -m "Add .nojekyll for GitHub Pages"
   git push origin main
   ```

2. **Verify build status:**
   ```bash
   MSYS_NO_PATHCONV=1 gh api repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages/builds/latest
   ```
   Look for `"status": "built"` and check for errors.

3. **Wait for deployment:**
   - GitHub Pages can take 1-5 minutes to deploy
   - Check build status again after waiting

4. **Clear browser cache:**
   - Press Ctrl+Shift+Delete (Windows) or Cmd+Shift+Delete (Mac)
   - Clear cached images and files
   - Try incognito/private mode

### Issue 2: Git Bash Path Rewriting Error

**Error:**
```
invalid API endpoint: C:/Program Files/Git/repos/...
Your shell might be rewriting URL paths
```

**Solution:**
Always use `MSYS_NO_PATHCONV=1` prefix with `gh api` commands on Git Bash:

```bash
# Wrong (on Git Bash):
gh api repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages

# Correct (on Git Bash):
MSYS_NO_PATHCONV=1 gh api repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages
```

### Issue 3: Root Index Not Redirecting

**Symptoms:**
- Blank page at root URL
- Hub page works when accessed directly

**Solution:**
Verify root index.html has redirect:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="refresh" content="0;url=commercial-services/">
<title>FCS Commercial Services</title>
</head>
<body>
<p>Redirecting to <a href="commercial-services/">Commercial Services</a>...</p>
</body>
</html>
```

### Issue 4: Changes Not Appearing on Live Site

**Solutions:**

1. **Check if commit was pushed:**
   ```bash
   git status
   ```
   Should say: "Your branch is up to date with 'origin/main'"

2. **Verify latest commit on GitHub:**
   ```bash
   git log --oneline -1
   ```
   Compare with GitHub repository

3. **Check build status:**
   ```bash
   MSYS_NO_PATHCONV=1 gh api repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages/builds/latest
   ```

4. **Trigger rebuild (if needed):**
   ```bash
   # Make a small change
   echo "<!-- trigger rebuild -->" >> README.md
   git add README.md
   git commit -m "Trigger rebuild"
   git push origin main
   ```

### Issue 5: Permission Denied or Authentication Failed

**Solutions:**

1. **Re-authenticate GitHub CLI:**
   ```bash
   gh auth login
   ```
   Follow prompts to authenticate

2. **Check SSH keys:**
   ```bash
   ssh -T git@github.com
   ```

3. **Use HTTPS instead of SSH:**
   ```bash
   git remote set-url origin https://github.com/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2.git
   ```

---

## Complete Command Reference

### Quick Reference: Full Deployment Process

```bash
# 1. CREATE REPOSITORY
gh repo create SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2 --public

# 2. PREPARE LOCAL DIRECTORY
cd /e/Downloads
mkdir fcs-commercial-v2
cd fcs-commercial-v2

# 3. COPY FILES
cp -r /path/to/source/* .

# 4. CREATE .nojekyll
touch .nojekyll

# 5. INITIALIZE GIT
git init
git add .
git commit -m "Initial commit: FCS Commercial Website V2"
git remote add origin https://github.com/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2.git
git push -u origin main

# 6. ENABLE GITHUB PAGES (Git Bash on Windows)
MSYS_NO_PATHCONV=1 gh api -X POST repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages \
  -f source[branch]=main \
  -f source[path]=/

# 7. VERIFY STATUS
MSYS_NO_PATHCONV=1 gh api repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages

# 8. CHECK BUILD
MSYS_NO_PATHCONV=1 gh api repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages/builds/latest

# 9. WAIT 1-2 MINUTES, THEN VISIT:
# https://syncshepherd-main.github.io/Claude_FCS_Commercial_Mockup_V2/
```

### Common Git Commands

```bash
# Check status
git status

# View commit history
git log --oneline -5

# View recent changes
git diff

# Add all files
git add .

# Commit changes
git commit -m "Your message here"

# Push to GitHub
git push origin main

# Force push (use carefully!)
git push -f origin main

# Pull latest changes
git pull origin main

# View remotes
git remote -v

# Check current branch
git branch
```

### GitHub CLI Commands

```bash
# Check authentication
gh auth status

# View repository
gh repo view SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2

# Open repository in browser
gh repo view SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2 --web

# List repositories
gh repo list SyncShepherd-Main

# Check Pages status (Git Bash)
MSYS_NO_PATHCONV=1 gh api repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages

# Check latest build (Git Bash)
MSYS_NO_PATHCONV=1 gh api repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages/builds/latest
```

---

## Best Practices

### Commit Messages

**Good commit messages:**
```bash
git commit -m "Add new drainage solutions page with case studies"
git commit -m "Update hub page FAQ section with 5 new questions"
git commit -m "Fix mobile navigation menu toggle"
git commit -m "Replace v4 with v5 structure - simplified to 13 pages"
```

**Bad commit messages:**
```bash
git commit -m "updates"
git commit -m "fix"
git commit -m "changes"
```

### File Organization

- Keep one `index.html` per directory
- Use lowercase with hyphens for directory names: `commercial-foundation-repair`
- Avoid spaces in filenames
- Keep structure flat (avoid deep nesting)

### Testing Before Push

1. **Test locally:** Open files in browser before pushing
2. **Check links:** Verify all navigation links work
3. **Validate HTML:** Use W3C validator if possible
4. **Test mobile:** Use browser dev tools to test responsive design

### Version Control

- Create meaningful commits for each logical change
- Don't commit generated files or large binaries
- Use `.gitignore` if needed
- Tag major versions: `git tag -a v2.0 -m "Version 2.0 release"`

---

## URLs and Links

### Repository URLs
- **Repository:** https://github.com/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2
- **Live Site:** https://syncshepherd-main.github.io/Claude_FCS_Commercial_Mockup_V2/
- **Hub Page:** https://syncshepherd-main.github.io/Claude_FCS_Commercial_Mockup_V2/commercial-services/

### API Endpoints
- **Pages Info:** `https://api.github.com/repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages`
- **Latest Build:** `https://api.github.com/repos/SyncShepherd-Main/Claude_FCS_Commercial_Mockup_V2/pages/builds/latest`

---

## For Next Version (V3, V4, etc.)

### Checklist for New Versions

- [ ] Create new repository with version number in name
- [ ] Prepare files in clean directory structure
- [ ] Add `.nojekyll` file
- [ ] Initialize git and push
- [ ] Enable GitHub Pages via API
- [ ] Verify build status
- [ ] Create README.md
- [ ] Test all pages and links
- [ ] Document any changes to this process

### Naming Convention

- V2: `Claude_FCS_Commercial_Mockup_V2`
- V3: `Claude_FCS_Commercial_Mockup_V3`
- V4: `Claude_FCS_Commercial_Mockup_V4`

---

## Summary

**What This Process Accomplishes:**
1. ✅ Creates GitHub repository
2. ✅ Organizes files with proper structure
3. ✅ Deploys to GitHub Pages
4. ✅ Makes site publicly accessible
5. ✅ Provides versioning and history
6. ✅ Documents everything for future use

**Total Time:** ~10 minutes (excluding file preparation)

**Result:** Fully deployed, publicly accessible website with version control and documentation.

---

**📅 Last Updated:** February 8, 2026
**✍️ Documented By:** Claude Code
**📝 Version:** 1.0

*Keep this guide updated with any process changes for future deployments.*
