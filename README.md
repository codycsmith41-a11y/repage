# RePage – Unscroll the Internet

> Infinite scroll steals up to 30% of your time. RePage puts it back.

[![Chrome Web Store](https://img.shields.io/badge/Chrome%20Web%20Store-Install%20Free-4361ee?style=flat-square&logo=googlechrome)](https://chromewebstore.google.com/detail/repage-unscroll-the-inter/bpenhlddapadgmhkijphelpokhaaianm)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

**[Install from Chrome Web Store →](https://chromewebstore.google.com/detail/repage-unscroll-the-inter/bpenhlddapadgmhkijphelpokhaaianm)**

---

## Why this exists

Engagement increases 15–50% when a UI switches from pagination to infinite scroll. Platforms know this — it is why the Next Page button disappeared from every major website.

That is not a coincidence. It is a dark pattern: a deliberate design choice that benefits the platform at the user's expense. [Research from Utrecht University](https://www.uu.nl/en/news/researchers-advise-the-house-of-representatives-education-needed-on-safe-screen-use-for-children) specifically highlights infinite scroll as disproportionately harmful to children and neurodivergent users. A [2026 study in *Social Media + Society*](https://phys.org/news/2026-02-social-media-addictive-clicking.html) identifies it as a primary mechanism of social media addiction — not content quality, but the structural removal of stopping points.

RePage is the counterweight. It puts the *page* back in *webpage*.

---

## What it does

Install RePage and every infinitely-scrolling page gets a numbered nav bar:

```
‹  1  2  3  …  47  ›
```

**Works on:** Reddit, Twitter/X, YouTube, Wikipedia, Gmail, ChatGPT, Gemini, LinkedIn, Facebook, Instagram — any website with a scrollable area.

Sub-scroll containers (Wikipedia TOC, ChatGPT conversation sidebar, chat contact lists) get their own smaller nav bar that scales to the container width.

---

## Features

| Feature | Description |
|---|---|
| **Pagination** | Numbered pages on every feed and article |
| **Keyboard shortcuts** | Z / X (right-hand mouse friendly) or ← → arrows |
| **Greyscale mode** | Renders the entire page in black & white |
| **Disable Autoplay** | Pauses all videos on page load |
| **Mute Notifications** | Hides unread badges and notification counts |
| **Hide Like Counts** | Removes social engagement metrics |
| **Text-Only mode** | Strips images and videos from social feeds |
| **Per-site disable** | Toggle RePage off for any domain |

---

## Keyboard shortcuts

| Action | Keys |
|---|---|
| Next page | `X` · `→` · `PgDn` |
| Previous page | `Z` · `←` · `PgUp` |
| First / Last | `Home` · `End` |

Shortcuts are disabled when focus is in any input, editor, or compose box.

---

## Site-specific handling

| Site | Approach |
|---|---|
| Reddit, Twitter/X | Gentle mode — respects virtual scroll list |
| YouTube | Targets `ytd-app` custom element |
| Instagram | Body-scroll mode |
| Facebook | `#scrollview` inner container |
| LinkedIn | `.scaffold-finite-scroll__content` |
| Google Search | `/search` path only — skips Maps, Docs, etc. |
| ChatGPT / Claude / Gemini | AI chat thread + sidebar conversation history |
| Wikipedia | Sticky TOC sidebar as sub-scroll container |

---

## Privacy

- Zero data collection
- No account required
- No external requests
- Permissions: `activeTab` + `storage` only

---

## Technical overview

RePage is a Manifest V3 content script (~2,650 lines, zero dependencies).

- **Shadow DOM bar** — closed Shadow DOM, invisible to page JS and site CSS
- **SPA navigation** — patches `history.pushState`/`replaceState` + `popstate` for route changes
- **Sub-scroll detection** — second pass finds nested scrollable panels; width-aware renderer (< 220px = arrows-only)
- **Form guard** — walks full DOM tree for `contentEditable` + ARIA roles before intercepting keyboard
- **Autoplay blocking** — `MutationObserver` catches dynamically-injected `<video>` elements

---

## Install

**[Chrome Web Store →](https://chromewebstore.google.com/detail/repage-unscroll-the-inter/bpenhlddapadgmhkijphelpokhaaianm)**

Or load unpacked from this repo: `chrome://extensions` → Developer mode → Load unpacked → select this folder.

---

## License

MIT — free forever, no strings.

---

*The browser extension is step one. The goal is to unscroll all tech.*
