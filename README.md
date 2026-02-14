# Romantic Digital Book PWA

A beautiful Progressive Web App that creates an intimate digital book experience, hidden behind an installation requirement.

## Features

- Hidden content that only reveals after installation to home screen
- Romantic heart landing page for browser visitors
- Smooth vertical scrolling with snap-to-page behavior
- Floating particle animations
- Optional background music with toggle control
- Optimized for iPhone Safari
- Fully functional offline with service worker
- Mobile-first, responsive design

## Setup Instructions

### 1. Generate App Icons

Open `public/generate-icons.html` in your browser, then right-click each canvas and save as:
- `icon-192.png`
- `icon-512.png`

Save both files in the `public/` directory.

### 2. Add Your Content

Place your image files in the `public/assets/` directory:

- `0.jpg` - Cover page
- `1.webp` through `52.webp` - Book pages
- `music.mp3` - Optional background music

The app works without images (shows placeholders) for testing.

### 3. Build the Project

```bash
npm install
npm run build
```

### 4. Deploy to GitHub Pages

**Option A: Deploy dist folder**
1. Push your code to a GitHub repository
2. Build the project locally
3. Go to repository Settings > Pages
4. Select "Deploy from a branch"
5. Choose "main" branch and "/dist" folder
6. Save and wait for deployment

**Option B: Use GitHub Actions**
Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches: [ main ]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: 18
      - run: npm install
      - run: npm run build
      - uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

### 5. Test the PWA

**In Browser:**
- Visit your GitHub Pages URL
- You'll only see a pulsing heart

**After Installation:**
- On iPhone: Tap Share > Add to Home Screen
- Open the app from your home screen
- The full book will be revealed

## How It Works

The app detects if it's running in standalone mode (installed to home screen). If not, it only shows the heart screen. This creates a "secret gift" experience where the content is hidden until the user installs it.

## Technical Details

- Pure HTML/CSS/JavaScript (no frameworks)
- PWA with full offline support
- Service worker for asset caching
- Lazy loading for images
- iOS-specific optimizations

## Browser Support

Optimized for:
- iPhone Safari (iOS 12+)
- Works on all modern mobile browsers
- Desktop browsers supported

## File Structure

```
/
├── index.html              # Main app file
├── manifest.json           # PWA manifest
├── service-worker.js       # Offline functionality
└── public/
    ├── icon-192.png       # App icon (192x192)
    ├── icon-512.png       # App icon (512x512)
    └── assets/
        ├── 0.jpg          # Cover image
        ├── 1.webp         # Page 1
        ├── ...            # Pages 2-52
        └── music.mp3      # Background music (optional)
```

## Customization

### Change Colors

Edit the gradients in `index.html`:
- `#heart-screen` - Landing page background
- `#book-container` - Book view background
- `.particle` - Floating particle colors

### Adjust Animations

Modify the animation durations in CSS:
- `.heart` pulse animation
- `.page` fade-in timing
- `.particle` floating speed

### Music Volume

Add this line after the bgMusic declaration:
```javascript
bgMusic.volume = 0.3; // 30% volume
```

## Tips for Best Results

1. Use high-quality images in WebP format for smaller file sizes
2. Keep the cover image (0.jpg) under 500KB
3. Optimize all images before uploading
4. Test on an actual iPhone for best experience
5. Use subtle, romantic background music (soft instrumental works best)

## License

Free to use for personal projects.
