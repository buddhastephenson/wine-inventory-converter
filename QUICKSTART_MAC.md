# Quick Start Guide for Mac Users

## Prerequisites (One-Time Setup)

### Install Git (if you don't have it)
Open Terminal and type:
```bash
git --version
```

If it says "command not found", install it:
```bash
# Install Homebrew (package manager) first
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Then install git
brew install git
```

## Step-by-Step Instructions

### 1. Find Your Downloaded File

The `.tar.gz` file is probably in your Downloads folder. Let's navigate there:

```bash
# Open Terminal (Applications > Utilities > Terminal)

# Go to Downloads folder
cd ~/Downloads

# Check if the file is there
ls -l wine-inventory-converter.tar.gz
```

You should see the file listed!

### 2. Extract the Archive

```bash
# Extract the file
tar -xzf wine-inventory-converter.tar.gz

# Go into the new folder
cd wine-inventory-converter

# See what's inside
ls -l
```

You should see:
- index.html
- README.md
- LICENSE
- And other files...

### 3. Test It Locally (Optional but Recommended!)

Before uploading anywhere, let's make sure it works:

```bash
# Open the HTML file in your default browser
open index.html
```

Your web app should open! Try uploading a wine list to make sure it works.

### 4. Set Up Git

**First time only** - tell Git who you are:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

Now initialize the repository:

```bash
# Make sure you're in the wine-inventory-converter folder
pwd  # Should show: /Users/yourname/Downloads/wine-inventory-converter

# Initialize git
git init

# Add all files
git add .

# Create your first commit
git commit -m "Initial commit: Wine Inventory Converter v1.0"
```

### 5. Create GitHub Repository

**In your web browser:**

1. Go to https://github.com
2. Sign in (or create account if new)
3. Click the **"+"** in top right corner
4. Click **"New repository"**
5. Fill in:
   - **Repository name:** `wine-inventory-converter`
   - **Description:** `Convert wine supplier price lists to standardized Excel format`
   - **Public** or **Private** (your choice)
   - ⚠️ **DO NOT** check "Add a README" or any other files
6. Click **"Create repository"**

GitHub will show you some commands. **Ignore them!** We'll use our own.

### 6. Connect Your Mac to GitHub

**Back in Terminal:**

```bash
# Replace YOUR_USERNAME with your actual GitHub username
git remote add origin https://github.com/YOUR_USERNAME/wine-inventory-converter.git

# For example:
# git remote add origin https://github.com/johnsmith/wine-inventory-converter.git

# Rename branch to 'main' (GitHub's default)
git branch -M main

# Push to GitHub!
git push -u origin main
```

**First time pushing?** GitHub will ask for your username and password.

⚠️ **Important:** GitHub no longer accepts passwords! You need a **Personal Access Token**.

#### How to Get a Token:

1. Go to https://github.com/settings/tokens
2. Click **"Generate new token (classic)"**
3. Give it a name: "Wine Converter Mac"
4. Check the **"repo"** scope (gives access to your repositories)
5. Click **"Generate token"** at bottom
6. **Copy the token** (looks like: ghp_xxxxxxxxxxxx)
7. **Save it somewhere safe!** You won't see it again

When Terminal asks for password, **paste your token** instead.

### 7. Verify on GitHub

1. Go to https://github.com/YOUR_USERNAME/wine-inventory-converter
2. You should see all your files there! 🎉

## Easiest Way to Host: Netlify

### Option A: Drag & Drop (No Terminal Needed!)

1. Go to https://app.netlify.com/drop
2. Sign up/sign in (can use GitHub account)
3. **Drag the entire `wine-inventory-converter` folder** onto the page
4. Wait 10 seconds
5. Done! You get a live URL like: `https://random-name-12345.netlify.app`

### Option B: Connect to GitHub (Auto-deploys on changes!)

1. Go to https://app.netlify.com
2. Click **"Add new site"** → **"Import an existing project"**
3. Choose **GitHub**
4. Select your `wine-inventory-converter` repository
5. Build settings:
   - Build command: (leave empty)
   - Publish directory: `/` (or leave default)
6. Click **"Deploy"**

Now every time you push to GitHub, it auto-updates your website! 🚀

## Alternative: GitHub Pages (Also Free!)

1. Go to your GitHub repository
2. Click **"Settings"** (top menu)
3. Click **"Pages"** (left sidebar)
4. Under "Source":
   - Branch: **main**
   - Folder: **/ (root)**
5. Click **"Save"**
6. Wait 1-2 minutes
7. Your site will be at: `https://YOUR_USERNAME.github.io/wine-inventory-converter/`

## Making Changes Later

After you change any files:

```bash
# Go to your project folder
cd ~/Downloads/wine-inventory-converter

# See what changed
git status

# Add changes
git add .

# Commit with a message describing what you changed
git commit -m "Added new supplier parser"

# Push to GitHub
git push
```

If you're using Netlify with GitHub connection, your website updates automatically!

## Troubleshooting

### "Permission denied" when pushing to GitHub
- You need to use a Personal Access Token, not your password
- Follow the token instructions above

### "Not a git repository"
- Make sure you're in the wine-inventory-converter folder
- Run: `pwd` to check your location
- Should be: `/Users/yourname/Downloads/wine-inventory-converter`

### Can't find the tar.gz file
```bash
# Search for it
cd ~
find . -name "wine-inventory-converter.tar.gz" 2>/dev/null
```

### Terminal shows "command not found"
- Make sure you're typing commands exactly as shown
- Check for typos
- Make sure Git is installed: `git --version`

## Getting Help

- **YouTube:** Search "how to use git and github mac"
- **GitHub Docs:** https://docs.github.com/en/get-started
- **Git Basics:** https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup

## Summary of What You've Done

1. ✅ Extracted the project files
2. ✅ Tested locally in browser
3. ✅ Initialized Git repository
4. ✅ Pushed to GitHub for version control
5. ✅ Deployed to Netlify (or GitHub Pages) for public access

You now have:
- **Source code on your Mac** (to make changes)
- **Backup on GitHub** (version control)
- **Live website** (for others to use)

Congratulations! 🎉🍷
