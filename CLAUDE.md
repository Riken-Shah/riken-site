# Riken Shah – Personal Site

## Project Overview
Static personal site for Riken Shah, deployed on Cloudflare Pages via GitHub auto-deploy. Single `index.html` with no build step.

- **Live URL**: https://riken.me
- **Repo**: https://github.com/Riken-Shah/riken-site
- **Hosting**: Cloudflare Pages (connected to GitHub, auto-deploys on push to `main`)
- **Domain**: riken.me (Cloudflare DNS), www.riken.me redirects to apex via Cloudflare Redirect Rule
- **Cloudflare Account**: Rikenshah.02@gmail.com (ID: ef44744f424f5bb00d8640febf528286)

## Architecture
- Pure static HTML — no framework, no build, no JS dependencies
- All CSS is inline in `<style>` block (no external stylesheets)
- Fonts: SF Pro Display + SF Pro Text loaded from jsdelivr CDN
- Favicon: Path-based SVG (not text-based) for consistent cross-device rendering, with PNG fallbacks at 16/32/180/192/512px
- OG image: 1200x630 PNG generated from SVG via `rsvg-convert`
- Resume PDF served from `/resume.pdf`

## Design Decisions
- **Apple-inspired aesthetic**: Clean, minimal, lots of whitespace. SF Pro fonts, subtle borders, muted secondary colors (#6e6e73, #86868b)
- **Navbar kept minimal**: Only "Resume" and "Get in Touch" — social links live in the hero section and footer instead of cluttering the nav
- **Get in Touch**: Uses `mailto:` link. The nav-cta class has explicit `color: var(--bg)` on hover to prevent the white text from being overridden by the generic `.topnav-right a:hover` rule
- **Stats grid**: 6 stats in a 3x2 grid. Downloads (800K+) and rating (4.8★) were originally one box but looked cramped — now 4.8★ is the headline with "800K+ Downloads" in the label below
- **Stat hover**: Shows "View ↗" in top-right corner on hover to signal clickability
- **Social icons**: Inline SVGs (not icon font) for GitHub, X/Twitter, LinkedIn, Dev.to, and email — keeps it zero-dependency
- **Experience section**: Collapsible accordion to keep the page scannable — work history is there but doesn't dominate
- **SEO/OG**: Full Open Graph + Twitter Card meta tags. `summary_large_image` card. Canonical URL set to https://riken.me
- **www redirect**: Handled by Cloudflare Redirect Rule (not `_redirects` file) since the site may be deployed as a Worker. CNAME for www points to riken.me, proxied through Cloudflare

## Files
- `index.html` — The entire site
- `resume.pdf` — Resume (source: ~/Downloads/resume-obsidian.pdf)
- `favicon.svg` — Vector favicon (path-based "R" on dark rounded square)
- `favicon-16.png`, `favicon-32.png` — PNG favicon fallbacks
- `apple-touch-icon.png` — 180px iOS home screen icon
- `icon-192.png`, `icon-512.png` — PWA manifest icons
- `og-image.png` — Social sharing preview image (1200x630)
- `site.webmanifest` — PWA manifest
- `_redirects` — Cloudflare Pages redirect rules (www → apex fallback)

## Workflow
- Edit `index.html`, commit, push to `main` — Cloudflare auto-deploys
- To regenerate favicons from SVG: `rsvg-convert favicon.svg -w SIZE -h SIZE -o OUTPUT.png`
- Cloudflare API calls use `CLOUDFLARE_ACCOUNT_ID=ef44744f424f5bb00d8640febf528286` env var
