### Notes from the author

> The system design follows a component-architecture approach, with a pinch of hope and dreams doing the heavy lifting for the 3D rendering. That code is a mess. Mapping GIFs, images, and videos onto Three.js objects meant stacking simultaneous tags on meshes just to get identifiers logged to the console, so I could work out which object needed changing and how to attach a component to it in place. Painful — and I learned a lot.
>
> — *wizard nazim*

The successor project fixes this with a cleaner separation of concerns.

This repo is kept as-is for reference.

> **Status:** This repository is an archived first-generation portfolio. It is no longer deployed. Development continues in a private, two-service distributed system at **[desclution.vercel.app](https://desclution.vercel.app/)**.

<!-- Badges: uncomment after adding a LICENSE file and confirming CI -->
<!-- ![License](https://img.shields.io/github/license/wizard-nazim/portfolio-void) -->
<!-- ![Last commit](https://img.shields.io/github/last-commit/wizard-nazim/portfolio-void) -->

---

A personal portfolio for **Nazim Rafudeen** — artist, musician, and developer based in Cape Town, South Africa. Built with Next.js 14, TypeScript, Tailwind CSS, and Three.js, with a vintage synthwave / newsprint aesthetic.

## Table of Contents

- [About](#about)
- [Project Status](#project-status)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Routes](#routes)
- [Key Features](#key-features)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [Authoring Content](#authoring-content)
- [Deployment](#deployment)
- [Known Issues & Roadmap](#known-issues--roadmap)
- [Contributing](#contributing)
- [License](#license)
- [Credits & Contact](#credits--contact)

---

## About

`portfolio-void` was the first version of my personal site published publicly. It collects four strands of work in one place:

- **Original music** — produced and released as *vetkat*
- **Visual art & collage**
- **Zine / writing** — MDX-based blog
- **Technical work** — React, TypeScript, .NET

It was also my learning ground: I used it to get to grips with how Three.js works and to try out creative ideas that didn't need to justify themselves — a zine section, a spinning vinyl player, and so on.



---

## Project Status

| | |
|---|---|
| **Repository** | Archived / reference only |
| **Live site** | No — deployment closed |
| **Former URL** | `portfolio-murex-beta-w3qzug647r.vercel.app` (offline) |
| **Current site** | [desclution.vercel.app](https://desclution.vercel.app/) |
| **Successor architecture** | Private repos, two services, self-hosted homelab server reachable over Tailscale |

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Framework** | Next.js 14 (App Router) |
| **UI** | React 18 |
| **Language** | TypeScript |
| **Styling** | Tailwind CSS · CSS Grid · CSS animations |
| **3D** | Three.js · React Three Fiber · Drei |
| **Content** | MDX (zine posts) |
| **Forms** | Formspree |
| **Deployment** | Vercel |
| **Analytics** | Vercel Analytics |

**Language composition:** TypeScript 63% · CSS 32.7% · MDX 3.9% · JavaScript 0.4%

---

## Project Structure

```
portfolio-void/
├── app/                          # Next.js App Router
│   ├── page.tsx                  # Homepage — hero + latest drops
│   ├── layout.tsx                # Root layout (Shell, fonts, globals)
│   ├── globals.css               # CSS variables, scanlines, base styles
│   ├── art/page.tsx              # Art gallery grid + lightbox
│   ├── music/page.tsx            # Disc player + tracklist
│   ├── zine/
│   │   ├── page.tsx              # Zine index with featured issue
│   │   └── [slug]/page.tsx       # Individual MDX post
│   ├── cv/page.tsx               # CV (HTML + PDF download)
│   └── contact/page.tsx          # Contact form + social links
├── src/
│   ├── components/               # Reusable React components
│   │   ├── Shell.tsx             # Global layout (logo, header, nav, footer)
│   │   ├── MagTitle.tsx          # "NAZIM" magazine letter tiles
│   │   ├── Ticker.tsx            # Scrolling header ticker
│   │   ├── NavSidebar.tsx        # Left navigation
│   │   ├── Footer.tsx            # Footer bar
│   │   ├── DiscPlayer.tsx        # Spinning vinyl player
│   │   ├── TrackList.tsx         # Music tracklist
│   │   ├── ArtGrid.tsx           # Art gallery layout
│   │   ├── ArtLightbox.tsx       # Full-screen image overlay
│   │   ├── ZineHero.tsx          # Featured zine card
│   │   ├── ZineList.tsx          # Issue index
│   │   ├── ContactForm.tsx       # Formspree contact form
│   │   ├── SocialCard.tsx        # Social link card
│   │   ├── HeroSceneWrapper.tsx  # Three.js 3D hero scene
│   │   └── mdx/                  # MDX custom components
│   │       ├── EmbedTrack.tsx    # SoundCloud / Spotify embeds
│   │       └── Pullquote.tsx     # Styled blockquotes
│   └── data/                     # Static data
│       ├── tracks.ts             # Music tracklist
│       ├── artworks.ts           # Art gallery items
│       ├── projects.ts           # Dev projects (CV)
│       └── site.ts               # Global site config
├── content/
│   └── zine/                     # MDX blog posts
│       ├── patience.mdx          # Seed post (Issue #4)
│       ├── issue-03.mdx
│       ├── issue-02.mdx
│       └── issue-01.mdx
├── public/                       # Static assets
│   ├── cv.pdf                    # CV download (placeholder)
│   ├── bg.gif                    # Homepage background
│   ├── homepage-gif.gif          # Hero fallback (2D)
│   └── images/
├── next.config.mjs
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

---

## Routes

| Route | Description |
|---|---|
| `/` | Homepage — hero with intro and latest drops (music, zine, dev) |
| `/art` | Art gallery with lightbox |
| `/music` | Disc player, track list, and SoundCloud embeds |
| `/zine` | Zine index — featured issue plus all posts with tag filters |
| `/zine/[slug]` | Individual post, rendered from MDX |
| `/cv` | CV — HTML resume plus PDF download |
| `/contact` | Social links and contact form |

---

## Key Features

### Disc Player

- Spinning vinyl with an animated tonearm
- Play/pause, previous/next, shuffle
- Track cover art display
- Visual progress bar
- Glow-ring animation while playing
- Integrated SoundCloud embeds

**Tracks:** Ｐａｔｉｅｎｃｅ (صبر) — 2025 single · Corner Shop — 2023 · ulontitled · upside down id · idea 2 · idea — 2025–26

### Design System

**Aesthetic:** indie / pop-art / vintage / synthwave / newsprint

```css
--color-bg:      #0a0a0a;  /* deep black */
--color-text:    #f0e6c8;  /* cream */
--color-accent:  #ff1aff;  /* hot pink */
--color-accent2: #ff6600;  /* orange */
--color-accent3: #ffcc00;  /* yellow */
```

**Typography**

- Display: Abril Fatface, Permanent Marker, Righteous
- Body: Special Elite
- UI labels: Courier Prime (monospace)

**Visual effects**

- Scanline overlay via `body::after`
- Magazine-style letter tiles (N / A / Z / I / M)
- Card hover states — rotate, lift, pink border
- Corner-fold decorations

### MDX Zine

Posts carry structured frontmatter:

```yaml
---
title: "Patience with your own process"
issue: 4
date: "2025-05-01"
tag: "Mood"          # Mood | Process | Playlist | Visual
excerpt: "..."
featured: true
---
```

Custom components available inside posts:

- `<EmbedTrack url="..." />` — SoundCloud or Spotify embed
- `<Pullquote>text</Pullquote>` — styled blockquote
- Standard Markdown images and lists

### Contact Form

Formspree-backed, with name, email, subject, and message fields, real-time validation, and success/error states. Submissions route to `nazim.dev@proton.me`.

---

## Getting Started

### Prerequisites

- **Node.js 18.17 or later** (Next.js 14 requirement)
- npm, pnpm, or yarn

### Install and run

```bash
git clone https://github.com/wizard-nazim/portfolio-void.git
cd portfolio-void
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

### Production build

```bash
npm run build
npm run start
```

### Lint

```bash
npm run lint
```

### Available scripts

| Script | Purpose |
|---|---|
| `npm run dev` | Local development server |
| `npm run build` | Production build |
| `npm run start` | Serve the production build |
| `npm run lint` | ESLint |

---

## Configuration

No environment variables are required for the core site to run.

**Formspree.** The form ID lives in `src/components/ContactForm.tsx`. Formspree IDs are public by design — they ship to the browser — but you should restrict submissions to your own domains in the Formspree dashboard so the endpoint can't be reused elsewhere. To swap in your own form, create one at [formspree.io](https://formspree.io) and replace the ID.

**Analytics.** Vercel Analytics activates automatically on Vercel deployments and needs no configuration.

**Assets.** `public/cv.pdf` is a placeholder. Replace it with your real CV; the `/cv` download link points at that file.

---

## Authoring Content

### Add a music track

Edit `src/data/tracks.ts`:

```typescript
export const tracks = [
  {
    id: 1,
    title: "Track Name",
    slug: "track-slug",
    year: 2025,
    tag: "Single",
    coverArt: "https://...",
    soundcloudUrl: "https://soundcloud.com/vetkat/...",
  },
];
```

### Add an artwork

Edit `src/data/artworks.ts`:

```typescript
export const artworks = [
  {
    id: 1,
    title: "Ｐａｔｉｅｎｃｅ (صبر) — Cover Art",
    type: "Cover Art",
    year: 2025,
    imageUrl: "https://...",
  },
];
```

### Write a zine post

Add a new `.mdx` file under `content/zine/`:

```mdx
---
title: "Post Title"
issue: 5
date: "2025-06-01"
tag: "Process"
excerpt: "Brief excerpt..."
featured: false
---

# Heading

Your content here.

<EmbedTrack url="https://soundcloud.com/vetkat/track" />

> Pull quote text

![Alt text](image.jpg)
```

---

## Deployment

The site targets Vercel:

1. Push the repository to GitHub.
2. Import it at [vercel.com](https://vercel.com).
3. Vercel detects the Next.js settings automatically.
4. Deploy — subsequent pushes to `main` redeploy automatically.

To attach a custom domain, use **Settings → Domains** in the Vercel dashboard and follow the DNS instructions.

---

## Known Issues & Roadmap

**Known issues**

- The music player is broken.
- The 3D hero scene code is difficult to maintain — object-to-component mapping relies on manually stacked mesh tags and console logging.
- `tsconfig.tsbuildinfo` is tracked in version control and should be ignored.

**Planned improvements**

- Refactor the Three.js scene into a declarative, data-driven structure.
- Add automated tests (none currently exist).
- Document accessibility behaviour — keyboard navigation, screen-reader support, and `prefers-reduced-motion` handling for the animations and 3D scene.
- Publish real Lighthouse results to back up the performance claims below.
- Move the Formspree form ID into an environment variable.

**Performance notes**

Pages are statically generated at build time, images are lazy-loaded through `next/image` with configured `remotePatterns`, and Vercel Analytics provides monitoring. *(Specific Lighthouse scores not yet recorded.)*

---

## Contributing

This repository is archived and not actively maintained, so pull requests are unlikely to be merged. If you spot something broken or want to discuss the approach, opening an issue is the best route.

If you fork it for your own portfolio, credit the original design.

---

## License

**No license file is currently included**, which means the default position applies: all rights reserved. If you intend others to reuse this code, add a `LICENSE` file — MIT is the usual choice for a project like this — and update this section accordingly.

---

## Credits & Contact

**Built by** Nazim Rafudeen · Cape Town, South Africa

- **Music** — [SoundCloud · vetkat](https://soundcloud.com/vetkat)
- **Visual** — [Instagram · @nazimrafudeen](https://www.instagram.com/nazimrafudeen/)
- **Code** — [GitHub · wizard-nazim](https://github.com/wizard-nazim)
- **Email** — nazim.dev@proton.me

Open to collaborations, commissions, and freelance projects.

*Handmade with ✦ in Cape Town.*
