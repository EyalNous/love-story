# Quick Start Guide

Get your Romantic Digital Book PWA up and running in 5 minutes!

## 1. Generate Icons (1 minute)

```bash
# Open this file in your browser:
open public/generate-icons.html
```

Right-click each canvas, "Save Image As...":
- Save as `public/icon-192.png`
- Save as `public/icon-512.png`

## 2. Add Your Images (2 minutes)

Drop your images into `public/assets/`:

Required:
- `0.jpg` - Your cover image

Optional (for testing, you can skip):
- `1.webp` to `52.webp` - Your page images
- `music.mp3` - Background music

**No images?** The app shows placeholders for testing!

## 3. Build & Test Locally (1 minute)

```bash
npm install
npm run build
npm run preview
```

Open the URL shown (usually http://localhost:4173)

## 4. Test PWA Behavior

**Browser View:**
- Should only show a pulsing heart

**Standalone Mode (simulated):**
- Open browser DevTools
- Toggle device toolbar (mobile view)
- Open DevTools settings (F1)
- Under "Devices", check "Add custom device"
- Add a device with `standalone` display mode

OR test on actual mobile device after deployment!

## 5. Deploy to GitHub (1 minute)

```bash
# Create repo on GitHub first, then:
git init
git add .
git commit -m "Initial commit"
git remote add origin YOUR_REPO_URL
git push -u origin main
```

Then:
1. Go to repo Settings > Pages
2. Source: Deploy from branch
3. Branch: `main` Folder: `/dist`
4. Save

Done! Visit your GitHub Pages URL in 1-2 minutes.

## Testing on iPhone

1. Visit your GitHub Pages URL
2. Tap Share button
3. "Add to Home Screen"
4. Open from home screen
5. The book should appear!

## Common Issues

**Icons not showing after install**
- Make sure both icon files are in `public/` before building
- Run `npm run build` again after adding icons

**Images not loading**
- Check files are in `public/assets/` folder
- Check file names match exactly: `0.jpg`, `1.webp`, etc.

**Heart still showing after install**
- Make sure you opened from home screen icon, not browser
- Try force-closing and reopening the app

## Next Steps

- Read `README.md` for full documentation
- Read `DEPLOYMENT.md` for detailed deployment guide
- Customize colors and animations in `index.html`

## Need Help?

Check the console for errors:
- Desktop: F12 > Console
- iPhone: Settings > Safari > Advanced > Web Inspector

Happy creating! ❤️
