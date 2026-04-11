---
project: about-page
stars: 17
description: |-
    Just a personal page
url: https://github.com/auroursa/about-page
---

# Cynosura

Personal website and blog, built with Astro and Tailwind CSS v4. Deployed on Cloudflare Pages.

## Features

- **Home** (`/`) — personal introduction, article timeline, skill/device panels, seasonal gallery, and music showcase
- **Blog** (`/posts`) — markdown articles with category filtering, RSS feed, and Disqus comments
- **Friends** (`/friends`) — curated links to friends' websites
- **About** (`/about`) — site milestones, tech stack, and color palette
- **OpenGraph** — auto-generated OG images for every page at build time via satori + sharp

## Project Structure

```
src/
├── assets/fonts/          # Overpass font files (woff2 + ttf)
├── components/            # Astro components
├── content/blog/          # Markdown blog posts
├── data/                  # Static data (friends, gallery, music, social links)
├── layouts/
│   └── BaseLayout.astro   # Shared layout with nav, drawer, and meta tags
├── pages/
│   ├── index.astro
│   ├── about.astro
│   ├── friends.astro
│   ├── 404.astro
│   ├── rss.xml.ts
│   ├── posts/
│   │   ├── index.astro
│   │   ├── [slug].astro
│   │   └── category/[category].astro
│   └── og/                # OG image endpoints (generated at build time)
│       ├── [slug].png.ts
│       ├── page/[page].png.ts
│       └── category/[category].png.ts
├── styles/                # CSS (global tokens, components, navigation)
└── utils/                 # Helpers (date, categories, OG image generation)
public/
├── img/                   # Static images and avatars
├── font/                  # Font license (OFL.txt)
└── js/                    # Client-side scripts
```

## Development

Requires Node.js 18+ and pnpm.

```bash
git clone git@github.com:auroursa/about-page.git
cd about-page
pnpm install
pnpm dev        # http://localhost:4321
```

Other scripts: `pnpm build` (production build), `pnpm preview` (preview build locally).

## Writing Posts

Create a `.md` file in `src/content/blog/` with frontmatter:

```markdown
---
title: Post Title
pubDate: 2024-01-22 09:41:00
description: Brief description
category: 日常
slug: post-slug
---
```

Categories in use: 日常, 杂谈, 技术.

## Deployment

Deployed to Cloudflare Pages. Build command: `pnpm build`, output directory: `dist`.

The legacy feed path `/posts/feeds/all.atom.xml` is redirected to `/rss.xml` via `public/_redirects`.

## License

Source code is licensed under the [MIT License](LICENSE).

The Overpass font is licensed under the [SIL Open Font License](public/font/OFL.txt).

