# GitHub Upload Guide - Operating Systems Coursework

Since Git is not installed on your system, here are **two methods** to upload your journal to GitHub:

---

## Method 1: GitHub Web Interface (Easiest - No Git Required)

### Step 1: Create a New Repository on GitHub

1. **Open your browser** and go to: https://github.com/login
2. **Log in** to your GitHub account
3. Click the **"+"** icon in the top-right corner
4. Select **"New repository"**
5. Fill in the details:
   - **Repository name:** `CourseworkOS-Journal` (or your preferred name)
   - **Description:** "Operating Systems CMPN202 Technical Journal"
   - **Visibility:** ✅ **Public** (required for GitHub Pages)
   - **DO NOT** initialize with README (we already have one)
6. Click **"Create repository"**

### Step 2: Upload Files via Web Interface

1. On your new repository page, click **"uploading an existing file"**
2. **Drag and drop** all files from `d:\CourseworkOS\Journal\` into the upload area:
   - index.md
   - week1.md through week7.md
   - README.md
   - QUICK_REFERENCE.md
3. **Create folders** for assets:
   - Click "Create new file"
   - Type: `assets/week1/.gitkeep`
   - Repeat for week2 through week7
4. Add a commit message: "Initial commit: OS Coursework Journal"
5. Click **"Commit changes"**

### Step 3: Enable GitHub Pages

1. Go to your repository **Settings** tab
2. Scroll down to **"Pages"** in the left sidebar
3. Under **"Source"**, select:
   - Branch: **main**
   - Folder: **/ (root)**
4. Click **"Save"**
5. Wait a few minutes, then your site will be available at:
   - `https://[your-username].github.io/CourseworkOS-Journal/`

---

## Method 2: Install Git and Use Command Line (Recommended for Future)

### Step 1: Install Git

1. Download Git from: https://git-scm.com/download/win
2. Run the installer (use default settings)
3. Restart your terminal/PowerShell

### Step 2: Configure Git

```powershell
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Step 3: Initialize and Push

```powershell
# Navigate to your Journal folder
cd d:\CourseworkOS\Journal

# Initialize Git repository
git init

# Add all files
git add .

# Commit files
git commit -m "Initial commit: OS Coursework Journal"

# Create repository on GitHub (via web), then:
git remote add origin https://github.com/[your-username]/CourseworkOS-Journal.git

# Push to GitHub
git branch -M main
git push -u origin main
```

---

## Quick Steps Summary (Method 1 - Web Upload)

1. ✅ Go to https://github.com/login
2. ✅ Log in to your account
3. ✅ Create new repository (public, named "CourseworkOS-Journal")
4. ✅ Upload all .md files from `d:\CourseworkOS\Journal\`
5. ✅ Enable GitHub Pages in Settings → Pages
6. ✅ Get your URL: `https://[username].github.io/CourseworkOS-Journal/`

---

## What to Submit on Moodle

After uploading to GitHub, create these files:

### File 1: `[StudentID]_GitHub_URL.txt`
```
https://[your-username].github.io/CourseworkOS-Journal/
```

### File 2: `[StudentID]_OSCoursework_Demonstration.mp4`
(Your 8-minute video demonstration)

---

## Files to Upload (Checklist)

From `d:\CourseworkOS\Journal\`:

- [ ] index.md
- [ ] week1.md
- [ ] week2.md
- [ ] week3.md
- [ ] week4.md
- [ ] week5.md
- [ ] week6.md
- [ ] week7.md
- [ ] README.md
- [ ] QUICK_REFERENCE.md
- [ ] assets/ folder (create on GitHub)

---

## Need Help?

If you encounter any issues:
1. Make sure your repository is **public** (for GitHub Pages)
2. Wait 2-3 minutes after enabling Pages for the site to build
3. Check the Pages section in Settings to see the deployment status

---

**I'm opening your browser to GitHub now. Follow Method 1 above to upload your files!**
