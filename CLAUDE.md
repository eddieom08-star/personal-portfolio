# Portfolio — Claude Code Context

## Project Overview
Personal portfolio site for IOAO Consulting. Single-page HTML (no framework, no build step) deployed to Vercel via GitHub repo `personal-portfolio`. Audiences: employers/recruiters, consulting clients, co-founders/investors.

## Owner Context
- **Name:**
- **Brand:** IOAO Consulting Ltd
- **Role:** AI Product Lead @ Parloa (Real-Time Communications) — phone carrier integrations, WebRTC, CCaaS, PCI payments, integration marketplace
- **Background:** 10+ years fintech — Grab (Grab Pay Card w/ Mastercard), VoxSmart (financial compliance AI), conversational AI
- **Consulting:** IOAO Consulting Ltd — fintech strategy, AI/automation, international expansion. Target: PE firms, Series A+ founders
- **Email:** idomile.omoniyi@gmail.com
- **LinkedIn:** https://www.linkedin.com/in/edo-o/
- **GitHub:** https://github.com/eddieom08-star
- **Location:** UK

## Tech Stack
- **Stack:** Vanilla HTML/CSS/JS — single `index.html`, no build tooling, no framework
- **Fonts:** Google Fonts — Cormorant Garamond (display), Syne (UI sans), Space Mono (labels/mono)
- **Deployment:** GitHub Pages (auto-deploys on push to `main`), custom domain `www.ioaoconsulting.com`
- **Images:** All screenshots embedded as base64 data URIs — no external image dependencies

## File Structure
```
/
├── index.html   ← entire site (HTML + CSS + JS + all images as base64)
├── CNAME        ← custom domain for GitHub Pages (www.ioaoconsulting.com)
├── CLAUDE.md    ← this file
└── README.md    ← brief GitHub description
```

## Design System
- **Nav logo + H1:** "IOAO Consulting"
- **Hero label:** "Product Lead · Fintech Founder · AI Builder & Consultant"
- **Palette:** `--bg: #080808`, `--bg-2: #111111`, `--bg-card: #141414`, `--border: rgba(255,255,255,0.07)`, `--text: #f0ece4`, `--text-muted: rgba(240,236,228,0.45)`, `--accent: #e8c547`
- **Per-project accent colours:** SemaSlim `#47c57a`, OpenClaw `#e85447`, RecoveryPath `#4788e8`, Trading Signals `#e8c547`, SME Ad Builder `#c547e8`, AI Accounting `#47b5e8`, Web Gen `#e87c47`
- **Custom cursor:** gold dot + lagging ring, scales on hover
- **Scroll reveal:** IntersectionObserver, `opacity 0→1` + `translateY(32px)→0`
- **Stack marquee:** CSS animation, content duplicated for seamless loop

## Contact & Links (live — do not change without instruction)
- **Email:** idomile.omoniyi@gmail.com
- **LinkedIn:** https://www.linkedin.com/in/edo-o/ (opens in new tab)
- **GitHub:** https://github.com/eddieom08-star (opens in new tab)
- **"Get In Touch" CTA:** mailto pre-filled — subject "Enquiry via IOAO Portfolio"
- **"Start a Conversation":** mailto pre-filled — subject "Consulting Enquiry via IOAO Portfolio"
- All contact links open email client directly — no backend required

## Projects (current state)

| Project | Size | Accent | Status | Screenshots |
|---|---|---|---|---|
| SemaSlim Companion | wide (8) | `#47c57a` | Active | 4 phone frames: Dashboard, Food Log, AI Recipes, Welcome |
| OpenClaw | narrow (4) | `#e85447` | Active | None |
| RecoveryPath | half (6) | `#4788e8` | Live | 6 phone frames: Welcome, Onboarding, Assessment, Home, Dashboard, AI Coach |
| Trading Signals Dashboard | half (6) | `#e8c547` | Active | 2 browser mockups: Options Signals, Index Options |
| SME Ad Builder | narrow (4) | `#c547e8` | Live | 2 browser mockups: Landing Page, Dashboard |
| AI Accounting Solution | wide (8) | `#47b5e8` | Concept | None — "Request Brief" mailto only |
| SME Web Generation Service | narrow (4) | `#e87c47` | Active | 1 browser mockup: Forge app |

## Screenshot Patterns

### Phone gallery (mobile apps)
```html
<div class="screenshot-gallery">
  <div class="screenshot-gallery-label">App Screens</div>
  <div class="screenshot-scroll">
    <div class="phone-wrapper">
      <div class="phone-frame">
        <div class="phone-notch"></div>
        <div class="phone-screen">
          <img src="data:image/png;base64,BASE64_HERE"
               style="width:100%;height:100%;object-fit:cover;object-position:top;border-radius:21px;"
               alt="Label"/>
        </div>
        <div class="phone-home-bar"></div>
      </div>
      <div class="screen-caption">Label</div>
    </div>
  </div>
</div>
```

### Browser mockup gallery (desktop apps)
```html
<div class="browser-mockup-label">App Screens</div>
<div class="screenshot-scroll" style="gap:16px;padding-bottom:12px">
  <div style="flex-shrink:0;width:300px">
    <div class="browser-mockup" style="margin-top:0">
      <div class="browser-chrome">
        <div class="browser-dots">
          <div class="browser-dot red"></div>
          <div class="browser-dot yellow"></div>
          <div class="browser-dot green"></div>
        </div>
        <div class="browser-bar">
          <span class="browser-bar-lock">🔒</span>
          <span class="browser-bar-url">app.example.com</span>
        </div>
      </div>
      <div class="browser-screen">
        <img src="data:image/png;base64,BASE64_HERE" alt="Label" style="max-height:240px"/>
      </div>
    </div>
    <div class="screen-caption" style="text-align:center;margin-top:8px">Label</div>
  </div>
</div>
```

To convert a screenshot to base64:
```bash
python3 -c "import base64; print(base64.b64encode(open('screenshot.png','rb').read()).decode())"
```

## CRITICAL — Safe File Editing
The file is ~2MB due to embedded base64 images. `sed` and `str_replace` truncate large files. Always use Python for any edit:
```python
with open('index.html') as f:
    html = f.read()
# make changes to html string
with open('index.html', 'w') as f:
    f.write(html)
```
After every write, verify: `html.count('</html>') == 1` and all 7 project names are present.

For large insertions (new screenshots), write in parts:
```python
parts = [before, new_gallery_html, after]
with open('index.html', 'w') as f:
    for part in parts:
        f.write(part)
```

## Common Tasks

**Add a new project:** Copy an existing `.project-card` block. Update `--project-color`, icon, status class, tagline, name, desc, stack tags, links. Grid classes: `wide` (span 8), `half` (span 6), `narrow` (span 4).

**Add screenshots:** Convert PNG to base64, use phone or browser mockup pattern above. All `.screenshot-scroll` elements get drag-to-scroll automatically via the JS at the bottom of the file.

**Update a link:** GitHub links all point to `https://github.com/eddieom08-star`. Update individual repo slugs when repos go public.

## Deployment
1. Repo: `personal-portfolio` on GitHub (`eddieom08-star/personal-portfolio`)
2. GitHub Pages enabled — deploys from `main` branch root
3. Push to `main` triggers auto-deploy
4. Custom domain: `www.ioaoconsulting.com` (configured via `CNAME` file)

## Domain
- **Active:** `www.ioaoconsulting.com`
- **DNS:** Point CNAME record for `www` to `eddieom08-star.github.io`
- **Apex redirect:** Configure `ioaoconsulting.com` A records to GitHub Pages IPs if needed

## Style Rules (do not break)
- Fonts: Cormorant Garamond / Syne / Space Mono only — never Inter, Roboto, Arial, system-ui
- Dark editorial palette only — no light themes, no purple gradients on white
- Custom cursor (`#cursor`, `#cursorRing`) must always be present
- All interactive elements must trigger cursor scale on mouseenter/mouseleave
- All new content blocks need the `reveal` class for scroll animation
- Mobile breakpoint `max-width: 900px` — grid cards collapse to `span 12`
- All assets as base64 data URIs — never reference external image URLs
