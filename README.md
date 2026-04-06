# Tyler Walters — Website
## File Structure & Next Steps

---

## FILE STRUCTURE

```
/
├── index.html          Landing page (scroll sequence + ENTER)
├── about.html          Artist Statement/s + Bio
├── work.html           All works with parallax boxes
├── contact.html        Contact form
├── cv.html             Curriculum Vitae
├── press.html          Press & Documentation (placeholder)
├── style.css           Shared stylesheet for all inner pages
│
└── assets/
    ├── skyty-frames/   SkyTy scroll sequence frames
    │   ├── frame001.jpg
    │   ├── frame002.jpg
    │   └── ... (up to frame080.jpg or however many you export)
    │
    ├── reel/
    │   ├── reel-strip.mp4        Cropped reel video (~1920×400px)
    │   └── reel-strip-poster.jpg Still frame for video poster
    │
    └── TylerWalters-CV.pdf       Downloadable CV
```

---

## ASSETS YOU NEED TO PREPARE

### 1. SkyTy Frame Sequence (for landing page scroll)
- Export individual frames from the SkyTy gesture video in Isadora
- Recommended: 60–120 frames covering the full arc (gathering → throwing → cloud → dissolve)
- Format: JPEG, quality ~85%, dimensions matching your video (e.g. 1920×1080)
- Naming: frame001.jpg, frame002.jpg, frame003.jpg ... (zero-padded to 3 digits)
- Place in: assets/skyty-frames/
- Update FRAME_COUNT in index.html to match your actual frame count

### 2. Reel Strip Video
- Export from Isadora at custom dimensions, approximately 1920×400px
- Format: MP4, H.264, good quality
- Place at: assets/reel/reel-strip.mp4
- Also export a single still frame as: assets/reel/reel-strip-poster.jpg

### 3. Vimeo Video Embeds
Replace each video placeholder in work.html with a Vimeo embed iframe:

```html
<!-- Replace this: -->
<div class="video-placeholder">
  <span>Video — SkyTy</span>
</div>

<!-- With this (using your actual Vimeo video ID): -->
<iframe src="https://player.vimeo.com/video/YOUR_VIDEO_ID?background=0&color=4A90D9&title=0&byline=0&portrait=0"
        frameborder="0"
        allow="autoplay; fullscreen; picture-in-picture"
        allowfullscreen>
</iframe>
```

### 4. Parallax Background Image
The inner pages use a blurred, dimmed SkyTy frame as ambient background.
Once frame sequence is exported, assets/skyty-frames/frame040.jpg
(or whichever frame shows the flour cloud at its fullest) will work well.

### 5. CV PDF
Place your PDF CV at: assets/TylerWalters-CV.pdf

---

## DEPLOYING TO NETLIFY (Step by Step)

### Step 1: Create a GitHub account
Go to github.com and sign up if you don't have an account.

### Step 2: Create a new repository
- Click the + icon → New repository
- Name it: tyler-walters-website (or similar)
- Set to Public
- Click Create repository

### Step 3: Upload your site files
- On the repository page, click "uploading an existing file"
- Drag all your files and the assets folder into the upload area
- Click "Commit changes"

### Step 4: Create a Netlify account
Go to netlify.com and sign up (free tier is sufficient).

### Step 5: Deploy from GitHub
- In Netlify dashboard, click "Add new site" → "Import an existing project"
- Choose GitHub, authorize Netlify, select your repository
- Leave build settings blank (this is a static site — no build command needed)
- Click "Deploy site"
- Your site will appear at a URL like: amazing-name-123456.netlify.app

### Step 6: Purchase your domain
Go to namecheap.com or domains.google.com
Search for tylerwalters.com — if available, purchase it (~$12/year)

### Step 7: Connect your domain to Netlify
- In Netlify: Site settings → Domain management → Add custom domain
- Enter tylerwalters.com
- Netlify will give you nameserver addresses
- In your domain registrar's settings, update the nameservers to Netlify's
- Wait up to 24 hours for DNS to propagate
- Netlify automatically provisions an HTTPS certificate (free)

### Step 8: Verify
Visit tylerwalters.com — your site should be live with HTTPS.

---

## UPDATING CONTENT LATER

To update any page (add a new work, update bio, etc.):
1. Open the relevant .html file in a text editor (TextEdit on Mac works, or VS Code)
2. Make your changes
3. Go to your GitHub repository
4. Click on the file you changed
5. Click the pencil (edit) icon
6. Paste your updated content
7. Click "Commit changes"
8. Netlify detects the change and updates your live site within ~30 seconds

---

## CONTACT FORM

The contact form currently has action="#" which means it doesn't actually send emails yet.
To make it functional, the simplest solution is Netlify Forms (free, no code needed):

Change the form opening tag in contact.html from:
```html
<form class="contact-form" action="#" method="post" novalidate>
```
To:
```html
<form class="contact-form" name="contact" method="POST" data-netlify="true">
```

Netlify will automatically handle form submissions and email them to you.
Set up notifications in: Netlify dashboard → Forms → Form notifications.

---

## VIRTUAL INSTALLATIONS (Kitchen Pas de Deux, Unsettler)

These will be separate HTML pages that run the installations directly in the browser.
Video files should be hosted on Cloudflare R2 (free tier) rather than directly
on Netlify to avoid bandwidth limits.

We will build these pages separately once video files are prepared.
Link them from work.html by adding a button/link alongside each work entry.

---

## NOTES ON BROWSER COMPATIBILITY

The scroll sequence (landing page) uses the HTML5 Canvas API — supported in all modern browsers.
Parallax effects use CSS transforms and IntersectionObserver — supported in all modern browsers.
The site is tested at screen widths from 360px (mobile) to 2560px (large desktop).
No external JavaScript libraries are used — the site loads very fast.
