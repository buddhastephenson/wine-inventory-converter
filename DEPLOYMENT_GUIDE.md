# Deployment Guide

Quick reference for deploying Wine Inventory Converter to GitHub and Google Cloud.

## GitHub Deployment

### Step 1: Initialize Repository

```bash
cd wine-inventory-converter
git init
git add .
git commit -m "Initial commit: Wine Inventory Converter v1.0"
```

### Step 2: Create GitHub Repo

Visit: https://github.com/new

Settings:
- Repository name: `wine-inventory-converter`
- Description: `Convert wine supplier price lists to standardized Excel format - 14 suppliers supported`
- Public ✓ (or Private if preferred)
- Do NOT initialize with README/LICENSE/.gitignore (we have them)

### Step 3: Push to GitHub

```bash
git remote add origin https://github.com/YOUR_USERNAME/wine-inventory-converter.git
git branch -M main
git push -u origin main
```

### Step 4: Enable GitHub Pages (Optional)

1. Go to repository Settings
2. Pages section
3. Source: Deploy from branch
4. Branch: main, folder: / (root)
5. Save
6. Your app will be live at: `https://YOUR_USERNAME.github.io/wine-inventory-converter/`

## Google Cloud Storage (Static Hosting)

### Prerequisites

```bash
# Install Google Cloud SDK
curl https://sdk.cloud.google.com | bash
exec -l $SHELL
gcloud init
```

### Deploy to Cloud Storage

```bash
# Create bucket (must be globally unique)
gsutil mb gs://wine-inventory-converter-YOUR-PROJECT-ID

# Upload files
gsutil -m cp -r * gs://wine-inventory-converter-YOUR-PROJECT-ID/

# Configure as website
gsutil web set -m index.html -e index.html gs://wine-inventory-converter-YOUR-PROJECT-ID

# Make public
gsutil iam ch allUsers:objectViewer gs://wine-inventory-converter-YOUR-PROJECT-ID
```

Access at: `https://storage.googleapis.com/wine-inventory-converter-YOUR-PROJECT-ID/index.html`

### Custom Domain (Optional)

```bash
# Verify domain ownership
gcloud domains verify YOUR-DOMAIN.com

# Create CNAME record
# CNAME: www.YOUR-DOMAIN.com → c.storage.googleapis.com

# Configure bucket
gsutil web set -m index.html gs://www.YOUR-DOMAIN.com
```

## Google Cloud Run (Dynamic Hosting)

### Create Dockerfile

Already included in project. Deploys Python HTTP server.

### Deploy

```bash
gcloud run deploy wine-converter \
  --source . \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated \
  --memory 512Mi
```

Access at the URL provided (e.g., `https://wine-converter-xxx-uc.a.run.app`)

## Firebase Hosting

### Setup

```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login
firebase login

# Initialize (in project directory)
firebase init hosting

# Select:
# - Use existing project or create new
# - Public directory: . (current directory)
# - Single-page app: No
# - GitHub deploys: Optional
```

### Deploy

```bash
firebase deploy --only hosting
```

Access at: `https://YOUR-PROJECT.web.app`

## Netlify (Easiest Static Hosting)

### Option 1: Drag & Drop

1. Visit: https://app.netlify.com/drop
2. Drag the `wine-inventory-converter` folder
3. Done! Live URL provided

### Option 2: CLI

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Deploy
cd wine-inventory-converter
netlify deploy --prod
```

### Option 3: GitHub Integration

1. Push to GitHub first
2. Visit: https://app.netlify.com
3. New site from Git
4. Select your repository
5. Build settings:
   - Build command: (leave empty)
   - Publish directory: /
6. Deploy!

Auto-deploys on every push to GitHub.

## Vercel (Alternative Static Hosting)

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
cd wine-inventory-converter
vercel

# Production
vercel --prod
```

## Recommended: GitHub + Netlify

Best combination:
1. **GitHub** for version control and collaboration
2. **Netlify** for hosting (free, fast, auto-deploys)

Setup:
1. Push to GitHub (see above)
2. Connect Netlify to GitHub repo
3. Every push auto-deploys!

## Environment Variables (If Needed)

For any hosting platform:

```bash
# Example: API keys (if you add features later)
API_KEY=your-key-here
```

Most platforms have dashboard settings for environment variables.

## Cost Estimates

- **GitHub Pages**: Free
- **Netlify**: Free tier (100GB bandwidth/month)
- **Vercel**: Free tier (100GB bandwidth/month)
- **Firebase Hosting**: Free tier (10GB storage, 360MB/day transfer)
- **Cloud Storage**: ~$0.026/GB storage + $0.12/GB egress
- **Cloud Run**: ~$0.00002400/request (free tier: 2M requests/month)

For a small app like this, all options will likely be **free** or under $5/month.

## Post-Deployment Checklist

- [ ] Test web app loads correctly
- [ ] Test file upload works
- [ ] Test conversion with each supplier
- [ ] Test download works
- [ ] Verify on mobile/tablet
- [ ] Set up custom domain (optional)
- [ ] Enable analytics (optional)
- [ ] Add link in README

## Updating After Deployment

### GitHub
```bash
git add .
git commit -m "Update: description of changes"
git push
```

### Netlify/Vercel (with GitHub integration)
Automatically updates on push!

### Cloud Storage
```bash
gsutil -m cp -r * gs://your-bucket/
```

### Cloud Run
```bash
gcloud run deploy wine-converter --source .
```

## Troubleshooting

### Files not found
- Check public directory settings
- Verify index.html is in root
- Check .gitignore isn't excluding files

### CORS errors
- For Cloud Storage, add CORS policy:
```bash
gsutil cors set cors.json gs://your-bucket
```

Where cors.json:
```json
[
  {
    "origin": ["*"],
    "method": ["GET", "HEAD"],
    "maxAgeSeconds": 3600
  }
]
```

### Build failures
- Check Node.js/Python versions
- Verify requirements.txt is correct
- Check for syntax errors

## Support

- GitHub Issues: Best for bug reports
- Stack Overflow: Tag with `wine-inventory-converter`
- Email: (your email if you want to provide support)

---

Good luck with deployment! 🚀🍷
