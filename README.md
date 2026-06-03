# Pockist Docs

A dark-themed Hugo documentation site for the Pockist project. Drop markdown files into the `content/` folder and Hugo auto-generates routes, a sidebar, and a homepage listing.

---

## Prerequisites

- **Hugo** extended version (tested with v0.123.7+; theme v9 requires minimum v0.68)
- **Git** (for submodule management)

Install Hugo: https://gohugo.io/installation/

---

## Getting Started

### 1. Clone the repo

```bash
git clone <repo-url>
cd pockist-docs
```

### 2. Initialize the theme submodule

The theme is tracked as a git submodule. After cloning, run:

```bash
git submodule update --init --recursive
```

This pulls the `hugo-book` theme into `themes/hugo-book/`.

### 3. Start the dev server

```bash
hugo server
```

Open `http://localhost:1313/` in your browser.

---

## Adding Content

### Drop a file in `content/`

```bash
echo '---
title: "My New Doc"
description: "What this doc covers"
weight: 20
---

# My New Doc

Your markdown here.' > content/my-new-doc.md
```

Hugo will:
- Auto-generate the route at `/my-new-doc/`
- Add it to the sidebar navigation
- Add it to the homepage flat list
- Apply dark syntax highlighting to code blocks

### Add a description

The homepage list uses the `description` frontmatter field as a subtitle. If you omit it, Hugo falls back to the page summary.

### Use subfolders (future)

```bash
mkdir content/architecture
echo '---
title: "Frontend"
---

# Frontend Architecture

...' > content/architecture/frontend.md
```

Hugo creates `/architecture/frontend/`, nests it in the sidebar, and the homepage still links to it.

---

## Frontmatter Cheat Sheet

```yaml
---
title: "Page Title"          # Required
description: "Subtitle"       # Optional — shown on homepage
date: 2026-06-02              # Optional
weight: 10                    # Optional — controls sidebar order (lower = first)
---
```

---

## Building for Production

```bash
hugo
```

This generates the static site into the `public/` directory. Deploy the contents of `public/` to any static host (GitHub Pages, Netlify, Vercel, S3, etc.).

---

## Project Structure

```
pockist-docs/
├── content/                  # All markdown content
│   ├── _index.md             # Homepage (must be named _index.md)
│   ├── db-and-components.md  # Existing doc
│   └── (add more here)
├── layouts/
│   └── index.html            # Custom homepage layout
├── themes/
│   └── hugo-book/            # Git submodule — docs theme
├── hugo.toml                 # Site config (dark mode, monokai, search, etc.)
└── README.md                 # This file
```

---

## Theme & Styling

- **Theme:** [Hugo Book](https://github.com/alex-shpak/hugo-book) (v9, dark mode)
- **Syntax highlighting:** Chroma with `monokai` style
- **Search:** Built-in Flexsearch, enabled
- **Sidebar:** Auto-generated from all content in `content/`
- **Table of contents:** Enabled on every page

---

## Updating the Theme

If you want to pull a newer version of the theme later:

```bash
cd themes/hugo-book
git fetch origin
git checkout <tag-or-branch>
cd ../..
```

Then verify compatibility and restart the server.

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| `Module "hugo-book" is not compatible` | Theme v9+ requires Hugo 0.158+ extended. Pin to an older tag or upgrade Hugo. |
| Sidebar is empty | Make sure `content/` has files and `hugo.toml` has `BookSection = '*'` |
| Theme missing after clone | Run `git submodule update --init --recursive` |
| `unexpected <with> in else` | Theme too new for your Hugo version. Checkout `v9` in `themes/hugo-book`. |

---

## Original File Reference

The original `db-and-components.md` (without Hugo frontmatter) is preserved in the repo root. The version Hugo renders is in `content/db-and-components.md`.
