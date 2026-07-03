# My Blog

A personal blog built with [Jekyll](https://jekyllrb.com) and the
[Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) theme — the
same setup used by grahamwatts.co.uk. It's a **static site**: Markdown files are
compiled to plain HTML. No database, no server-side code. Search runs entirely
in the browser via Lunr.

## Prerequisites

This project uses the Homebrew Ruby (the macOS system Ruby is too old). Ruby was
installed with `brew install ruby`. Because it's keg-only, add it to your PATH.
Add this line to your `~/.zshrc` so every new terminal picks it up:

```sh
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
```

Then open a new terminal, or run `source ~/.zshrc`.

## Running locally

```sh
bundle install          # once, to install gems (already done)
bundle exec jekyll serve # build + live-reload server
```

Then open <http://localhost:4000>. Edits to posts/pages rebuild automatically;
refresh the browser to see them. Stop the server with Ctrl-C.

## Writing a post

Create a file in `_posts/` named `YEAR-MONTH-DAY-title.md`, e.g.
`2026-08-01-my-trip.md`, starting with front matter:

```markdown
---
title: "My Trip"
date: 2026-08-01 09:00:00 +0100
categories:
  - travel
tags:
  - photos
excerpt: "One-line summary shown in listings and search."
---

Your post content in **Markdown** goes here.
```

## Project layout

| Path                  | What it is                                            |
| --------------------- | ----------------------------------------------------- |
| `_config.yml`         | Site-wide settings (title, author, search, theme skin)|
| `_posts/`             | Your blog posts (Markdown)                             |
| `_pages/`             | Standalone pages (About, Search, archives)            |
| `_data/navigation.yml`| The top menu bar                                       |
| `index.html`          | Home page (paginated list of latest posts)            |
| `assets/`             | Your own images/CSS overrides (create as needed)      |
| `_site/`              | Generated output — never edit; it's rebuilt each time |

## Customising the look

- **Colour scheme:** change `minimal_mistakes_skin` in `_config.yml`
  (try `dark`, `mint`, `sunrise`, `contrast`, …).
- **Your details:** edit the `author:` block in `_config.yml` and
  `_pages/about.md`.
- **Avatar:** drop a photo at `assets/images/bio-photo.jpg`.
- Full theme docs: <https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/>

## Publishing (free hosting)

Any of these host the generated static site for free:

- **GitHub Pages** — push this repo; set `remote_theme: mmistakes/minimal-mistakes`
  in `_config.yml` if you hit plugin limits. Site lives at `you.github.io`.
- **Netlify / Cloudflare Pages** — connect the repo; build command
  `jekyll build`, publish directory `_site`. Supports all plugins and custom
  domains with automatic HTTPS.
