# Bhanu Cheepurupalli — Portfolio Site

A three-page personal portfolio for a policy generalist (digital rights · governance · human-rights accountability). Hand-built static HTML — **no framework, no build step**. Designed to be published free on GitHub Pages and edited by hand (or with an AI assistant) in small pieces.

> **New to this project / picking it up in a fresh chat?** Read **`Handover Document.html`** first — it has the full decision log, backlog, and a copy-paste context block. **`Design Guide.html`** has the exact colors, fonts, and voice rules. This README is the quick technical reference.

---

## The pages

| File | Role | Aesthetic |
|---|---|---|
| `Profile.html` | **Home.** Index-card hero, "front desk" intent router, skills↔experience cross-link, slim contact band (full bio lives on About.html). | *Field Notes* — composed, cream + ink |
| `Work.html` | Press-archive of selected work, live AI-oversight tracker embed, indexed CV. | *Press Archive* — editorial, poster headlines |
| `Play.html` | Draggable scrapbook pinboard — research questions, reading, radar, fun facts, guest pins. | *Collage* — loud, indigo + marigold |
| `About.html` | Standalone literary bio — portrait, first-person story, "Currently," languages, writing, contact. | *Field Notes* — clean single column |
| `GitHub Pages Guide.html` | Plain-English publishing walkthrough (for Bhanu, not for the repo). | Field Notes |
| `Design Guide.html` | The design system + voice/tone rules. | Field Notes |
| `Handover Document.html` | Strategy, decisions, backlog, resume-in-new-chat block. | Field Notes |

**Loudness is a deliberate dimmer switch:** Profile (composed) → Work (editorial) → Play (loud). Same type system throughout; color and energy rise across the three.

### `publish/` folder
A **ready-to-upload copy** for GitHub Pages. The home page is renamed `index.html` and every internal link points to `index.html` instead of `Profile.html`. Contents:

```
publish/
  index.html      ← Profile (home)
  Work.html
  Play.html
  About.html
  assets/         ← logos + all images
```

When you change a source page, regenerate its `publish/` twin (copy the file, then replace `Profile.html` → `index.html` inside it). See "Editing" below.

### Exploration archive (not part of the live site)
`Strategy Brief.html`, `Design Directions.html`, `Visual Options.html`, `Type Round 2.html` — early option-exploration docs kept for reference. Safe to ignore or delete; **do not publish them.**

---

## File tree

```
/
├── Profile.html              # home (source)
├── Work.html
├── Play.html
├── About.html
├── GitHub Pages Guide.html
├── Design Guide.html
├── Handover Document.html
├── README.md
├── assets/
│   ├── mark-eye.png          # primary logo (the eye mark)
│   ├── kali-lavender.png     # logo variants (lavender is used on Play)
│   ├── kali-indigo.png
│   ├── kali-purple.png
│   ├── kali-terracotta.png
│   └── work/
│       ├── headshot.jpg              # used in Profile › About
│       ├── cambodia-steps.jpg        # Play image-pin + Work gallery
│       ├── cambodia-temple.jpg       # Work gallery (Lower Mekong)
│       ├── graduation.jpg            # (available, unused)
│       ├── amnesty-12hoa.png         # Work gallery
│       ├── therapeutic-landscapes.png
│       ├── envirolab-scallops.png
│       ├── unicef-advocacy.png
│       ├── unicef-evaluating.png     # Work gallery (UNICEF blog)
│       ├── unicef-header.png
│       ├── academic-hgt.png          # Work › Academic & Curious
│       └── academic-kerala.png       # Work › Academic & Curious
├── publish/                  # ready-to-upload GitHub Pages copy
│   ├── index.html
│   ├── Work.html
│   ├── Play.html
│   ├── About.html
│   └── assets/
└── uploads/                  # raw source files (originals; not deployed)
```

---

## Tech notes

- **Pure static HTML + CSS + vanilla JS.** No npm, no bundler, no React. Open any file directly in a browser.
- **Fonts** load from Google Fonts via `<link>` in each page's `<head>`: Instrument Serif, Gloock, Big Shoulders Display, Bricolage Grotesque, Courier Prime, Space Mono, Caveat. (Requires internet; see Design Guide for the role of each.)
- **CSS is per-page**, inside a `<style>` block in `<head>`. All three pages share the same `:root` custom-property palette — keep them in sync if you change a token. (Full token list in `Design Guide.html`.)
- **JS is per-page**, inside `<script>` blocks at the end of `<body>`. No shared JS file.
- **All links are relative** (`Work.html`, `assets/...`). Never use absolute paths — they break on GitHub Pages.
- Inline-styles-only is **not** required here (that constraint was for the old free WordPress.com Custom-HTML workaround). On GitHub Pages, the `<style>`/`<script>` blocks work fine.

### Interactive features
| Page | Feature | How it works |
|---|---|---|
| Profile | **Front desk** intent router | Click a `.cnc-opt` → JS swaps `#cncResult` with 3 tailored cards from the `DATA` object. |
| Profile | **Skills ↔ Experience** | Click a `.skill` chip → JS highlights matching `.xrow` rows in the Experience list (via the `MAP` object) and dims the rest. |
| Work | **Live tracker embed** | `<iframe>` of `https://bhanurl.github.io/AIWI_civictriage/index.html`. If that URL moves, update the `src`. |
| Play | **Draggable pinboard** | Pointer-events drag; positions saved to `localStorage`. Tap (no drag) opens the side panel. |
| Play | **Guest pins** | Form writes a pin object to `localStorage` and renders it. **Local to one browser only** — see Backlog. |

### localStorage keys (Play only)
- `play_pos_v1` — `{ pinId: {x,y} }` saved pin positions.
- `play_guest_v1` — array of guest-submitted pin objects.

Bump the `_v1` suffix if you ever change the pin data shape and want to invalidate old saves. The **↺ Reset board** button clears `play_pos_v1` only.

### Editing pin content (Play)
All pins live in the `PINS` array near the top of the `<script>` in `Play.html`. Each pin:
```js
{ id:"r1", c:"research", x:40, y:30,
  t:"Title", teaser:"one-liner", body:"panel text",
  link:"Work.html", linkText:"See it" }   // link optional
// image pin:  { id, c, x, y, t, img:"assets/...", cap:"caption" }
```
`c` (category) ∈ `research | reading | radar | me | aesthetics | guest` — controls color + filter. `x`/`y` are default positions on the 1080-wide board.

---

## Editing & publishing

**To edit:** open the source `.html` file, change it, preview in a browser.

**To re-publish after a change:**
1. Copy the changed source file into `publish/` (Profile becomes `publish/index.html`).
2. Inside that `publish/` copy, replace every `Profile.html` with `index.html`.
3. Drag the contents of `publish/` into the GitHub repo (see `GitHub Pages Guide.html`), commit.

Live URL: **https://bhanurl.github.io**

---

## Backlog / known limits

- **Guest pins are device-local.** Real shared submissions need a tiny free backend (Formspree / Google Form / Netlify Forms). Documented in the Handover.
- **Play reading/radar pins are prompts, not real content** — populate with Bhanu's actual reading list, favorites, and people/media on radar.
- **Work › report charts** — placeholder slot for the in-progress AI-governance research report; add charts when ready.
- **CV** is "on request" (intentionally — Bhanu distills rather than posting the raw file). No PDF is wired up yet.
- **Custom domain** (`bhanucheepurupalli.com`) not set up; GitHub Pages supports it for free if wanted.

---

*Built collaboratively in an AI design tool. Voice and tone are deliberate — read the voice rules in `Design Guide.html` before rewriting any copy.*
