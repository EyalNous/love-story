# Deployment Guide for GitHub Pages

This guide will walk you through deploying your Romantic Digital Book PWA to GitHub Pages.

## Prerequisites

1. A GitHub account
2. Git installed on your computer
3. Node.js installed (for building the project)

## Step-by-Step Deployment

### Step 1: Prepare Your Content

1. Generate icons:
   - Open `public/generate-icons.html` in a browser
   - Right-click each canvas and "Save Image As..."
   - Save as `icon-192.png` and `icon-512.png` in the `public/` folder

2. Add your images to `public/assets/`:
   - `0.jpg` - Cover image
   - `1.webp` through `52.webp` - Book pages
   - `music.mp3` - Background music (optional)

### Step 2: Build the Project

```bash
npm install
npm run build
```

This creates a `dist/` folder with all production files.

### Step 3: Create GitHub Repository

1. Go to https://github.com/new
2. Create a new repository (e.g., "romantic-book")
3. Don't initialize with README

### Step 4: Push Code to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

### Step 5: Enable GitHub Pages

**Option A: Manual Deployment (Simpler)**

1. Go to your repository on GitHub
2. Click "Settings" > "Pages"
3. Under "Build and deployment":
   - Source: "Deploy from a branch"
   - Branch: `main`
   - Folder: `/dist`
4. Click "Save"
5. Wait 1-2 minutes for deployment
6. Your site will be at: `https://YOUR_USERNAME.github.io/YOUR_REPO/`

**Option B: GitHub Actions (Automatic)**

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Build
        run: npm run build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

Then:
1. Commit and push this file
2. Go to Settings > Pages
3. Source: "GitHub Actions"
4. The workflow will run automatically on every push

### Step 6: Test Your PWA

1. Visit your GitHub Pages URL
2. You should see only a pulsing heart
3. On mobile (iPhone):
   - Tap the Share button
   - Select "Add to Home Screen"
   - Name it and add
4. Open from home screen
5. The full book should now be revealed

## Troubleshooting

### Icons not showing
- Make sure `icon-192.png` and `icon-512.png` are in `public/` folder before building
- Rebuild the project: `npm run build`

### Images not loading
- Check that images are in `public/assets/` folder
- Verify file names: `0.jpg`, `1.webp`, `2.webp`, etc.
- Images must be present before building

### Service Worker not working
- PWAs require HTTPS (GitHub Pages provides this automatically)
- Clear browser cache and reload
- Check browser console for errors

### App doesn't detect standalone mode
- Make sure you added it to home screen correctly
- Try closing and reopening the app
- Check that manifest.json is accessible at `/manifest.json`

## Updating Content

To update images or content:

1. Replace files in `public/assets/`
2. Run `npm run build`
3. Commit and push changes
4. GitHub Pages will automatically update

## Custom Domain (Optional)

1. Buy a domain from any registrar
2. Add a `CNAME` file to `public/` with your domain:
   ```
   yourdomain.com
   ```
3. In your domain registrar, add these DNS records:
   ```
   A    185.199.108.153
   A    185.199.109.153
   A    185.199.110.153
   A    185.199.111.153
   ```
4. In GitHub Settings > Pages, enter your custom domain
5. Wait 24-48 hours for DNS propagation

## Performance Tips

1. Optimize images before adding them:
   - Use https://squoosh.app for compression
   - Target: 200-300KB per image

2. WebP format is recommended for smaller file sizes

3. Keep music file under 3MB for faster loading

4. Test on actual iPhone for best experience

## Security Note

All assets are public once deployed. Don't include:
- Personal information
- Private photos you don't want public
- Sensitive content

Remember: Anyone with the link can view the heart screen, but content is only revealed after installation.
