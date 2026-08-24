# Himanshu Gautam — Developer Portfolio

> "You are not looking at a résumé. You are stepping into his development environment."

A terminal-inspired, editorial personal portfolio for **Himanshu Gautam (Himie)** — 2nd-year B.Tech CSE student at Amrita School of Computing, Coimbatore. Built as a code-editor-flavored interface: tabbed navigation reads like open files, sections read like commands, and the site's own supplied ASCII artwork sits at the center of the hero as its primary visual identity.

Live concept: `~/himanshu` — explore the site the way you'd explore a project on disk.

---

## Features

- **ASCII-driven hero** — the supplied ASCII artwork rendered as the site's signature visual, auto-scaled per breakpoint, with a restrained amber accent and soft reveal animation (skips animation entirely under `prefers-reduced-motion`).
- **Editor-tab navigation** — the top nav mimics open file tabs (`about.md`, `projects/`, `stack.json` …) and tracks scroll position via `IntersectionObserver`.
- **Project Explorer** — projects are presented as a file browser (list + detail panel) rather than a card grid, each with problem → solution → tech → learning, plus an embedded process-flow visualization.
- **Achievements gallery** — all six certificates/badges as a tappable grid with an expandable modal preview (touch-friendly, no hover dependency required).
- **Skills as data** — rendered as a styled `stack.json` terminal block. No fake proficiency percentages.
- **Fully responsive** — intentional layouts at 320px, 768px, 1024px, 1440px+, not a scaled-down desktop view.
- **Accessible** — semantic landmarks, visible focus states, alt text on every image, honors `prefers-reduced-motion`.
- **Two small easter eggs** — a console signature message, and number keys `1–7` jump between sections.

---

## Tech Stack

| Layer       | Choice                                  |
|-------------|------------------------------------------|
| Framework   | Next.js 14 (App Router) + TypeScript     |
| Styling     | Tailwind CSS (custom design tokens)      |
| Animation   | Framer Motion (scroll reveals only)      |
| Fonts       | Space Grotesk (display), Inter (body), JetBrains Mono (terminal) — via `next/font/google` |
| Images      | `next/image` with local static assets    |

No backend, no database, no GitHub API calls at runtime — all content is local and data-driven so the site loads fast and never depends on rate limits.

---

## Project Structure

```
src/
├── app/
│   ├── layout.tsx        # fonts, metadata/SEO
│   ├── page.tsx           # assembles all sections
│   └── globals.css        # design tokens, terminal chrome, a11y
├── components/
│   ├── navigation/        # EditorTabBar, StatusBar
│   ├── hero/               # Hero, AsciiIdentity, TerminalPrompt
│   ├── about/
│   ├── projects/           # Projects, ProjectExplorer
│   ├── skills/
│   ├── journey/
│   ├── achievements/
│   ├── leadership/
│   ├── contact/
│   └── shared/             # SectionHeading, Reveal, Footer, EasterEgg
├── data/                   # identity, projects, skills, journey, achievements, ascii
├── lib/                    # nav config, small utils
└── types/                  # shared TS interfaces
public/
├── ascii/himie.txt         # source ASCII artwork (also inlined in data/ascii.ts)
└── certificates/           # all certificate/badge images
```

All content lives in `src/data/*.ts` — to update a project, achievement, or skill, edit the data file, not the component.

---

## Local Setup

Requires Node.js 18.17+.

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

```bash
npm run build   # production build
npm run start   # serve the production build locally
npm run lint    # ESLint
```

> Note: `next/font/google` fetches font files at build time and needs internet access. If you're building in a fully offline/sandboxed environment, either allow the `fonts.googleapis.com` / `fonts.gstatic.com` domains, or swap `src/app/layout.tsx` to self-hosted fonts.

## Environment Variables

None required. The site has no API keys, secrets, or external integrations — everything is static, local data.

---

## Deployment

The project is a standard Next.js app and deploys cleanly to any Next.js-compatible host:

**Vercel (recommended)**
```bash
npm i -g vercel
vercel
```
Or connect the repo at [vercel.com/new](https://vercel.com/new) — zero config needed.

**Any Node host**
```bash
npm run build
npm run start
```

**Static export** — the site currently has no dynamic routes or server code, so it's also export-friendly if you'd prefer a fully static host (Netlify, GitHub Pages, etc.): add `output: "export"` to `next.config.mjs` and run `npm run build`.

Before going live, update `siteUrl` in `src/app/layout.tsx` to your real domain (used for Open Graph metadata).

---

## Future Improvements

- Optional curated GitHub API integration (selected repos, cached, with local fallback) if `github.com/marathonengineer` activity is worth surfacing later.
- Case-study depth pages per project if the project list grows beyond what the explorer panel comfortably holds.
- Light self-hosted font fallback for fully offline builds.
