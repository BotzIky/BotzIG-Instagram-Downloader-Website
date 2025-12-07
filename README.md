# Instagram Downloader - Download Reels, Photos & Videos

A fast, responsive, and easy-to-use Instagram downloader web application (BotzIG) that allows you to download reels, photos, and videos in high quality.

---

## 🌟 Features

- **Download Reels & Videos (MP4)**  
  Download Instagram reels and videos in MP4 format with a single click.

- **Download All Photos in a Post**  
  For carousel posts, all images are displayed in a gallery view with individual download buttons.

- **Post Metadata Display**  
  Shows:
  - Post title / caption
  - Username
  - Original Instagram link
  - Likes count
  - Comments count
  - Post date

- **Comments Preview**  
  Displays several top comments (username + text) from the post.

- **Fully Responsive**  
  Optimized for desktop, tablet, and mobile devices.

- **Dark Theme UI**  
  Modern dark mode design following the TikBotz UI style:
  - Same header and footer structure
  - Same layout spacing and components
  - Mobile hamburger navigation

- **No Registration Required**  
  Completely free to use without any signup.

---

## 🚀 Demo

(Replace this with your live URL once deployed)

```text
https://instagram.botzaku.eu.org
```

---

## 🖼️ UI / UX

The Instagram downloader page reuses the same UX and UI patterns from the TikTok downloader:

- Same **navigation bar** (Docs, Tools, Uploader, Other, Terms, Privacy)
- Same **footer** (BotzApi branding + social links)
- Same **dark theme** and accent color (`#98ff98`)
- Same **input card** layout (title, description, URL input, Download button)
- Responsive **grid cards** for download options and galleries

Differences:

- Branding updated to **BotzIG**
- Icon updated to Instagram style
- Content and labels adapted to Instagram (reels, posts, photos)

---

## 🛠️ Technologies Used

- **HTML5** – Semantic markup
- **CSS3** – Modern styling with Flexbox and Grid (no framework)
- **JavaScript (ES6+)** – `async/await`, `fetch` API
- **Bootstrap Icons** – Icon library
- **SweetAlert2** – Beautiful toast/alert notifications
- **BotzApi** – Backend API for Instagram content fetching

---

## 📋 API Integration

This application uses the BotzApi Instagram downloader endpoint:

```http
GET https://host.optikl.ink/download/instagram?url={INSTAGRAM_URL}
```

### Example Photo/Carousel Response

```json
{
  "creator": "@PaxSenix",
  "ok": true,
  "message": "Hope you guys love my hard work :3",
  "detail": {
    "title": "#CatatanSepekan edisi 1 s.d. 7 Desember 2025",
    "source": "https://www.instagram.com/p/DR9rcTAjzkg/",
    "shortcode": "DR9rcTAjzkg",
    "comments": [
      {
        "text": "🇮🇩❤️🤍",
        "username": "niken_linggarwati26"
      }
    ],
    "comment_count": 53,
    "like_count": 890,
    "taken_at": 1765113700,
    "username": "sekretariat.kabinet"
  },
  "downloadUrls": [
    {
      "url": "https://...heic",
      "thumb": "https://...heic",
      "type": "heic",
      "name": "HEIC",
      "ext": "heic"
    }
  ]
}
```

### Example Video/Reel Response

```json
{
  "creator": "@PaxSenix",
  "ok": true,
  "message": "Hope you guys love my hard work :3",
  "detail": {
    "title": "follow @402withlovee.__ ...",
    "source": "https://www.instagram.com/reel/DRgOmRWktnx/",
    "shortcode": "DRgOmRWktnx",
    "comments": [
      {
        "text": "semoga semua rasa sayang...",
        "username": "creamyfavv"
      }
    ],
    "comment_count": 489,
    "like_count": 237041,
    "taken_at": 1764125528,
    "username": "402withlovee.__"
  },
  "downloadUrls": [
    {
      "url": "https://...mp4",
      "thumb": "https://...jpg",
      "type": "mp4",
      "name": "MP4",
      "ext": "mp4"
    }
  ]
}
```

### How The Frontend Uses The API

- Input: User pastes an `https://www.instagram.com/p/...` or `https://www.instagram.com/reel/...` URL
- The page sends a GET request to:

  ```javascript
  const apiUrl =
    'https://host.optikl.ink/download/instagram?url=' + encodeURIComponent(url);
  const res = await fetch(apiUrl);
  const data = await res.json();
  ```

- On success (`data.ok === true`), the UI displays:
  - Title, username, likes, comments, date
  - For multiple media (`downloadUrls.length > 1`): gallery grid with thumbs and per-item download buttons
  - Download cards for each media (`MP4` for videos, `HEIC/JPG` for images)

- Downloads:
  - Files are downloaded via `fetch` → `blob()` → temporary link using the browser, or fall back to just opening the URL in a new tab if needed.

---

## 🎯 How to Use

1. **Copy Instagram URL**
   - Open Instagram app or website
   - Go to the reel, video, or post you want to download
   - Copy the share link (e.g. `https://www.instagram.com/reel/...` or `https://www.instagram.com/p/...`)

2. **Paste URL**
   - Open the BotzIG Instagram downloader page
   - Paste the Instagram URL into the input field
   - Click the **Download** button

3. **View Details**
   - See the post title, username, stats, and comments preview
   - For carousel posts, view all images in a grid gallery

4. **Choose Download Option**
   - For **video/reel**: Download MP4 file
   - For **photo/carousel**: Click download on each image thumbnail
   - Each media item has its own download button

5. **Download Complete**
   - Files will be saved by your browser
   - Use **“Download Another”** to start over

---

## 💻 Installation (Local)

1. Clone the repository where this Instagram page lives (or the TikBotz repo if you added it there):

```bash
git clone https://github.com/BotzIky/TikBotz-TikTok-Downloader-Website.git
cd TikBotz-TikTok-Downloader-Website
```

2. Add your `index-instagram.html` (or similar) file to the project root.

3. Serve locally (optional, but recommended for testing CORS and layout):

```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx http-server
```

4. Open in browser:

```text
http://localhost:8000/index-instagram.html
```

---

## ☁️ Deployment

### GitHub Pages

1. Commit and push your Instagram downloader page to the repo.
2. Go to **Settings > Pages**.
3. Select:
   - Branch: `main`
   - Folder: `/ (root)`
4. Click **Save**.
5. Your site will be live at:

```text
https://yourusername.github.io/TikBotz-TikTok-Downloader-Website
```

(You can link or redirect that to your Instagram-specific page.)

### Vercel

```bash
npm i -g vercel
vercel
```

Follow the prompts and set your entry page as needed.

### Netlify

1. Drag and drop the project folder into Netlify, **or**
2. Connect the GitHub repository and auto-deploy.

---

## 🔧 Configuration

### Change API Endpoint

If you move or proxy the API, update the URL in the JavaScript:

```javascript
const apiUrl =
  'https://host.optikl.ink/download/instagram?url=' + encodeURIComponent(url);
```

### Change Icon / Branding

- Icon URL used for BotzIG:

  ```html
  <link
    rel="icon"
    href="https://cdn.botzaku.eu.org/19VTQf9EF92QrDX_i4Hiduhi7bMnZoLNb"
  />
  ```

- Navbar logo text:

  ```html
  <span>BotzIG</span>
  ```

### Customize Colors

If you plan to refactor into CSS variables, you could use:

```css
:root {
  --primary-color: #98ff98;
  --primary-color-soft: #7ae87a;
  --bg-color: #000;
  --text-color: #f1fdf1;
}
```

And then swap the hard-coded values inside your `index-instagram.html`.

---

## 📱 Browser Support

- ✅ Chrome (latest)
- ✅ Firefox (latest)
- ✅ Safari (latest)
- ✅ Edge (latest)
- ✅ Opera (latest)
- ✅ Mobile browsers (iOS Safari, Chrome Mobile, Samsung Internet)

---

## ⚠️ Legal Disclaimer

This tool is provided for **personal use only**. Please ensure you have the rights to download and use any content.

- Respect Instagram’s Terms of Service and community guidelines
- Do not use downloaded content for commercial purposes without permission
- Always credit the original creator when reposting
- Respect intellectual property and privacy rights

BotzIG / BotzApi is an **unofficial** tool and is **not affiliated** with Instagram or Meta.

---

## 🤝 Contributing

Contributions are welcome. To contribute:

1. Fork the repository
2. Create your feature branch:

   ```bash
   git checkout -b feature/AmazingFeature
   ```

3. Commit your changes:

   ```bash
   git commit -m "Add AmazingFeature for Instagram downloader"
   ```

4. Push to the branch:

   ```bash
   git push origin feature/AmazingFeature
   ```

5. Open a Pull Request

Ideas:

- Add multi-language support
- Add theme toggle (dark/light)
- Add batch download for multiple Instagram URLs
- Add download history

---

## 🐛 Bug Reports

If you find a bug, please open a GitHub issue with:

- Description of the bug
- Steps to reproduce
- Expected behavior
- Actual behavior
- Screenshots (if possible)
- Browser and OS information

---

## 👨‍💻 Author

**BotzAku (Riski Yanda)**

- Website: <https://botzaku.eu.org>
- Instagram: [@botzaku](https://instagram.com/botzaku)
- TikTok: [@botzaku](https://tiktok.com/@botzaku)
- Twitter/X: [@botz_aku](https://twitter.com/botz_aku)
- Telegram: [BotzAku](https://t.me/BotzAku)
- WhatsApp: [Channel](https://whatsapp.com/channel/0029VbBjxQl8qIzmg51J5W3x)
- Discord: [Server](https://discord.gg/Ehr7DrsU)

---

Made with ❤️ by [BotzAku](https://botzaku.eu.org)
