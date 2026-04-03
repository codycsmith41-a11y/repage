# RePage — Unscroll the Internet

> Browse the web in pages, like reading a book. Free, open source, no tracking.

Infinite scroll is broken by design — it hijacks your attention, makes it impossible to know where you are, and traps you in a feed with no end. **RePage fixes that.**

Install it once. Every website — Facebook, Instagram, LinkedIn, Reddit, YouTube, ChatGPT, any page — gets converted into numbered pages with a clean navigation bar at the bottom.

---

## What it does

- **Numbered pages on every site** — window scroll, inner-scroll containers, chat threads, sidebars, all of it
- **Keyboard navigation** — `Z`/`←`/`PgUp` for previous, `X`/`→`/`Space`/`PgDn` for next, `Home`/`End` for first/last
- **Mini bars for sub-scrollers** — chat histories, contact lists, table of contents, sidebars all get their own pagination
- **Instant page switches** — no smooth-scroll animation, no lag
- **Shadow DOM encapsulation** — the bar is invisible to page JavaScript, can't be detected or patched by sites
- **Bonus features**: greyscale filter, hide like counts, mute notification badges, text-only mode, disable autoplay

## Screenshots

| Wikipedia (93 pages) | Wikipedia TOC sub-bar |
|---|---|
| ![Main bar](https://raw.githubusercontent.com/codycsmith41-a11y/repage/main/screenshots/main-bar.png) | ![Sub bar](https://raw.githubusercontent.com/codycsmith41-a11y/repage/main/screenshots/sub-bar.png) |

## Install

**Chrome Web Store** — coming soon

**Manual install (Developer Mode):**
1. Download or clone this repo
2. Open `chrome://extensions`
3. Enable **Developer mode** (top right)
4. Click **Load unpacked** → select this folder

## Keyboard shortcuts

| Action | Keys |
|---|---|
| Next page | `X`, `→`, `Space`, `PgDn` |
| Previous page | `Z`, `←`, `PgUp` |
| First page | `Home` |
| Last page | `End` |

## How it works

RePage injects a content script at `document_start` on every page. It:
1. Calculates total page count from `scrollHeight / viewportHeight`
2. Locks `overflow: hidden` on `html`/`body` and uses `scrollTo()` / `scrollTop` for instant position jumps
3. Renders a fixed pagination bar in a **closed Shadow DOM** (invisible to page scripts)
4. Wraps `history.pushState`/`replaceState` on SPAs to re-initialise on navigation
5. Scans for sub-scroll containers (chat panels, sidebars, TOCs) and gives them their own mini bar

## Sites with special handling

| Site | Method |
|---|---|
| Instagram | `document.body.scrollTo()` (body is the scroll container) |
| YouTube | `ytd-app` inner container |
| Facebook | `#scrollview` + SPA navigation |
| LinkedIn | `.scaffold-finite-scroll__content` + SPA navigation |
| ChatGPT / Gemini | AI chat mode — starts on last page (most recent), paginates up |
| Twitter / X / Reddit / TikTok | Gentle mode — CSS `top` offset to preserve IntersectionObserver |

## Privacy

- No analytics, no telemetry, no data collection
- No network requests
- Permissions: `storage` (save settings), `activeTab` + `tabs` (detect current site for popup)

## License

MIT — free to use, fork, and modify.

---

*RePage is a side project. If it saves you time, consider [supporting on Patreon](https://www.patreon.com/joshforall).*
