# ⚡ TWA Generator

> Turn any website into an installable Android app (TWA) + PWA — powered by your choice of AI.

A single-file, mobile-first web app that generates all the config files you need for a **Trusted Web Activity (TWA)** and **Progressive Web App (PWA)**. Import your `index.html`, pick an AI provider, and download 10 ready-to-deploy files in one tap.

---

## ✨ Features

- 📱 **Mobile-first UI** — optimized for phones, works on desktop too
- 🎨 **12 built-in themes** — 6 dark + 6 light with auto-detect from system preference
- 🤖 **13 AI providers** — OpenRouter, Google Gemini, OpenAI, xAI Grok, DeepSeek, Groq, Mistral, Anthropic Claude, Together AI, Perplexity, Fireworks AI, Cerebras, and any OpenAI-compatible endpoint
- 🔑 **API key saved locally** — persisted in `localStorage`, never sent anywhere except directly to your chosen AI provider
- 🔌 **Test API button** — verifies the connection before generating, shows latency in ms
- 📁 **Import `index.html`** — auto-extracts `<title>` and `<meta name="description">`
- 🖼️ **Icon generator** — Canvas (letter + gradient) or upload your own (auto-resized to 192 & 512)
- 🔧 **Auto-inject TWA** — patches your `index.html` with manifest link, meta tags, apple-touch-icon, and service worker registration
- 🎨 **Theme Color Auto (Runtime)** — syncs the status bar color to the user's system theme in real time via `matchMedia`
- 📋 **Live activity log** — timestamped, color-coded, real-time feedback
- 📦 **Download files individually** or **download all** in one batch
- 🪶 **Zero backend** — everything runs client-side in your browser

---

## 📦 Files It Generates

| File | Purpose |
|---|---|
| `icon-192.png` | Home screen icon |
| `icon-512.png` | Splash screen / Play Store icon |
| `index.html` | Your original file + injected TWA tags (optional) |
| `manifest.json` | PWA manifest (name, icons, start_url, theme_color) |
| `serviceworker.js` | Offline caching (cache-first assets, network-first HTML) |
| `assetlinks.json` | Digital Asset Links — verifies domain ownership on Android |
| `privacy.html` | Privacy policy page |
| `terms.html` | Terms of service page |
| `vercel.json` | Vercel deployment config (headers, MIME types) |
| `netlify.toml` | Netlify deployment config (headers, redirects) |

---

## 🚀 How to Use

### 1. Import your `index.html`
Tap the file picker or drag & drop your HTML file. The app auto-detects:
- `<title>` → fills "Nama Aplikasi" & "Short Name"
- `<meta name="description">` → fills "Deskripsi Aplikasi"

### 2. Configure AI
Pick a **provider** and **model**, paste your **API key**, then tap **🔌 Test API** to verify.

> 💡 **Free tip:** Use [OpenRouter](https://openrouter.ai) with a `:free` model like `google/gemini-2.0-flash-exp:free` — no cost, no quota limits for this kind of task.

### 3. Fill in app info
| Field | Example | Notes |
|---|---|---|
| Nama Aplikasi | `My Awesome App` | Full name |
| Short Name | `MyApp` | Max 12 chars |
| URL / Domain | `https://myapp.com` | Must be HTTPS |
| Deskripsi Aplikasi | `A simple app for...` | 50–150 chars ideal |
| Package Name | `com.example.myapp` | Android reverse-domain |
| SHA-256 Fingerprint | `AA:BB:...` | Optional, from `keytool -list -v` |

### 4. Choose icon source
- **🔤 Letter** — auto-generates gradient + letter via Canvas
- **📤 Upload** — provide your own PNG/JPG/WebP (min 512×512)

### 5. Generate
Toggle **Inject TWA** and **Theme Color Auto**, then tap **⚡ Generate Semua File**. Download each file or all at once.

---

## 🛠️ Deployment

### Vercel
1. Deploy your project (the generated `vercel.json` handles headers)
2. Place `assetlinks.json` at `/.well-known/assetlinks.json`
3. Verify: `https://yoursite.com/.well-known/assetlinks.json`

### Netlify
1. Deploy the project (`netlify.toml` handles headers)
2. Place `assetlinks.json` at `/.well-known/assetlinks.json` or use the redirect in `netlify.toml`

### Android (Bubblewrap / Android Studio)
1. Use [Bubblewrap CLI](https://github.com/GoogleChromeLabs/bubblewrap) or Android Studio to build your TWA
2. Get your app's SHA-256:
   ```bash
   keytool -list -v -keystore mykeystore.jks -alias myalias
