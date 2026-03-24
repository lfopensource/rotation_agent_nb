# 🍌 Image Rotation Agent

> An AI-powered image rotation tool built on a 3-module agent architecture — LLM brain, OpenCV executor, and Nano Banana Pro (Gemini) inpainting.

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Powered by Gemini](https://img.shields.io/badge/Powered%20by-Nano%20Banana%20Pro-blue)
![No backend](https://img.shields.io/badge/Backend-None%20(runs%20in%20browser)-green)

---

## ✨ What it does

Upload any image, describe what you want in plain English, and the agent handles the rest:

- **"Rotate 40° counter-clockwise and fill the corners"**
- **"Flip the image horizontally"**
- **"Tilt 30° clockwise for a cinematic angle"**

The agent processes your instruction through three coordinated modules and returns a real, downloadable rotated image.

---

## 🏗️ Architecture

```
User Prompt
     │
     ▼
┌─────────────────┐     params      ┌──────────────────┐     rotated img     ┌─────────────────────┐
│  Module 1       │ ──────────────► │  Tool 1          │ ──────────────────► │  Tool 2             │
│  LLM Brain      │                 │  OpenCV Runner   │                     │  Nano Banana Pro    │
│  (Claude Sonnet)│                 │  (Canvas API)    │                     │  (Gemini API)       │
└─────────────────┘                 └──────────────────┘                     └─────────────────────┘
     Parses natural language,            Applies pixel-accurate                Fills rotated corners
     extracts direction, angle,          rotation using affine                 via AI Inpainting /
     and inpainting intent               transform math                        Outpainting
```

### Module 1 — LLM Brain (Claude Sonnet)
Receives the user's natural language instruction and extracts structured parameters:
- Rotation direction (`clockwise` / `counterclockwise` / `flip_h` / `flip_v`)
- Angle in degrees
- Whether inpainting is needed
- A fill prompt for the inpainting model

### Tool 1 — OpenCV Runner (Browser Canvas API)
Performs pixel-accurate rotation using affine transform math — equivalent to `cv2.getRotationMatrix2D` + `cv2.warpAffine` in Python OpenCV. The bounding box is expanded correctly so no content is clipped at non-90° angles.

### Tool 2 — Nano Banana Pro (Gemini API)
Calls `gemini-2.0-flash-preview-image-generation` to fill the blank triangular corners left by rotation. Uses your own Gemini API key — no data is stored or sent anywhere except directly to Google's API.

---

## 🚀 Usage

This is a **single HTML file** — no install, no build step, no backend.

### Option A: Open locally
```bash
# Just double-click index.html, or:
open index.html
```

### Option B: Host on GitHub Pages
1. Fork this repo and make it **public**
2. Go to Settings → Pages → Deploy from `main` branch
3. Visit `https://yourusername.github.io/rotation-agent`

### Option C: Any static host
Drop `index.html` onto Netlify, Vercel, Cloudflare Pages, or any static host.

---

## 🔑 API Keys

You need **two API keys** to use all features:

| Key | Where to get it | Used for |
|-----|----------------|----------|
| **Anthropic API key** | [console.anthropic.com](https://console.anthropic.com) | LLM Brain (parameter extraction) |
| **Gemini API key** | [aistudio.google.com/apikey](https://aistudio.google.com/apikey) | Nano Banana Pro inpainting |

Both keys are entered in the UI and **never leave your browser** — they go directly to each provider's API. Nothing is logged or stored.

> If no Gemini key is provided, the tool still works — it applies real pixel rotation and skips the inpainting step.

---

## 📋 Features

- ✅ Real pixel rotation (not just CSS transform)
- ✅ Correct clockwise / counter-clockwise direction
- ✅ Expanded bounding box for non-90° angles (no clipping)
- ✅ AI corner fill via Nano Banana Pro (Gemini inpainting)
- ✅ Before / after comparison panel
- ✅ One-click PNG download of result
- ✅ Live agent pipeline log
- ✅ Quick preset prompts
- ✅ No backend, no sign-up, fully client-side

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| UI | Vanilla HTML / CSS / JS |
| Fonts | Plus Jakarta Sans, DM Mono (Google Fonts) |
| LLM | Claude Sonnet via Anthropic API |
| Image rotation | Browser Canvas API (affine transform) |
| Inpainting | Gemini `gemini-2.0-flash-preview-image-generation` |
| Hosting | GitHub Pages (static) |

---

## 📄 License

MIT — see [LICENSE](./LICENSE) for details.

---

## 🙏 Credits

- [Nano Banana / Gemini](https://deepmind.google/technologies/gemini/) by Google DeepMind
- [Claude](https://anthropic.com) by Anthropic
- UI design inspired by the Nano Banana product aesthetic
