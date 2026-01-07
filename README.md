# IDGT Fitness - Progressive Web App

**Conditioned To Last**

A personalized workout tracking Progressive Web App that works offline and can be installed on any device.

## Features

- ✅ **Multi-User Profiles** - Create personalized workout plans for different users
- ✅ **Smart Setup Wizard** - Customizes workouts based on injuries and preferences
- ✅ **Multiple Workout Splits** - Push/Pull/Legs, Upper/Lower, Body Part, Full Body
- ✅ **Offline Support** - Works completely offline once installed
- ✅ **Progress Tracking** - Monthly calendar and streak tracking
- ✅ **Favorites System** - Save your go-to exercises
- ✅ **3x10-12 Rep Tracking** - Perfect for strength and hypertrophy
- ✅ **Injury-Friendly** - Specialized plans for ACL, shoulder, and back injuries

## Installation

### Desktop (Chrome, Edge, Brave)
1. Open `workout-tracker.html` in your browser
2. Click the install icon (➕) in the address bar
3. Click "Install"

### iOS (Safari)
1. Open `workout-tracker.html` in Safari
2. Tap the Share button
3. Scroll down and tap "Add to Home Screen"
4. Tap "Add"

### Android (Chrome)
1. Open `workout-tracker.html` in Chrome
2. Tap the three dots menu
3. Tap "Add to Home Screen" or "Install App"
4. Tap "Install"

## Creating App Icons

The included `icon.svg` needs to be converted to PNG files at different sizes. You can use online tools like:
- https://realfavicongenerator.net/
- https://www.favicon-generator.org/

Required icon sizes:
- icon-72.png (72x72)
- icon-96.png (96x96)
- icon-128.png (128x128)
- icon-144.png (144x144)
- icon-152.png (152x152)
- icon-192.png (192x192) - Required
- icon-384.png (384x384)
- icon-512.png (512x512) - Required

## Hosting

To use as a PWA, you need to host these files on a web server (with HTTPS):

### Quick Options:
1. **GitHub Pages** (Free)
   - Create a GitHub repository
   - Upload all files
   - Enable GitHub Pages in settings
   - Access via `https://yourusername.github.io/repo-name/workout-tracker.html`

2. **Netlify** (Free)
   - Drag and drop the folder to Netlify
   - Get instant HTTPS URL

3. **Vercel** (Free)
   - Connect your GitHub repo
   - Auto-deploys on push

4. **Firebase Hosting** (Free)
   - `firebase init hosting`
   - Deploy with `firebase deploy`

## Local Testing

To test the PWA locally with service workers:

```bash
# Using Python 3
python -m http.server 8000

# Using Node.js
npx http-server -p 8000
```

Then visit: `http://localhost:8000/workout-tracker.html`

**Note:** Service workers require HTTPS in production (but work on localhost for testing).

## File Structure

```
idgt-fitness/
├── workout-tracker.html    # Main app file
├── manifest.json          # PWA manifest
├── service-worker.js      # Offline functionality
├── icon.svg              # Source icon
├── icon-*.png            # Generated icons (you need to create these)
└── README.md             # This file
```

## Browser Support

- ✅ Chrome/Edge (Desktop & Mobile)
- ✅ Safari (iOS 11.3+)
- ✅ Firefox (Desktop & Mobile)
- ✅ Samsung Internet
- ✅ Opera

## Data Storage

All workout data is stored locally in your browser using `localStorage`:
- Profile information
- Workout history
- Completed workouts
- Favorites

**Note:** Data persists even when offline. Clearing browser data will remove all workout history.

## Updates

When you update the app:
1. Change the `CACHE_NAME` in `service-worker.js` (e.g., `idgt-fitness-v2`)
2. The service worker will automatically update on next visit
3. Users will get the new version without reinstalling

## Support

For issues or feature requests, create an issue in the repository or contact support.

---

**IDGT Fitness** - Track. Progress. Conquer. 💪
