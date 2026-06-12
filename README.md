# new home
https://codeberg.org/tannerr/my-docs


# My Docs

A dark-themed Hugo documentation site. Drop markdown files into `content/` folders and Hugo auto-generates routes, a sidebar, a grouped homepage, and section index pages.

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
cd my-docs
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

### Drop a file in an existing folder

```bash
echo '---
title: "My New Doc"
description: "What this doc covers"
weight: 20
---

# My New Doc

Your markdown here.' > content/javascript/my-new-doc.md
```

Hugo will:
- Auto-generate the route at `/javascript/my-new-doc/`
- Add it to the sidebar navigation under **JavaScript**
- Add it to the **JavaScript** section on the homepage
- Add it to the `/javascript/` section index page
- Apply dark syntax highlighting to code blocks

### Create a new section (folder)

```bash
mkdir content/architecture
echo '---
title: "Architecture"
---

# Architecture

Docs about system architecture.' > content/architecture/_index.md

echo '---
title: "Frontend"
description: "How the frontend is structured"
---

# Frontend Architecture

...' > content/architecture/frontend.md
```

Hugo will:
- Create `/architecture/frontend/` automatically
- Add **Architecture** as a new heading on the homepage
- Nest it in the sidebar navigation
- Create a section index page at `/architecture/` listing all pages inside

### Add a description

The homepage and section index pages use the `description` frontmatter field as a subtitle. If you omit it, only the title is shown.

---

## Frontmatter Cheat Sheet

```yaml
---
title: "Page Title"          # Required
description: "Subtitle"       # Optional — shown on homepage & section indexes
date: 2026-06-02              # Optional
weight: 10                    # Optional — controls order (lower = first)
---
```

---

## Ordering Content

Hugo sorts both **sections** (folders on the homepage) and **pages** inside each section using the same rules:

1. **`weight`** — lower numbers appear first (e.g., `weight: 10` before `weight: 20`)
2. **`date`** — newer items come first if no weight is set
3. **`title`** — alphabetical, if neither weight nor date is set

### Control section order on the homepage

Add `weight` to each section's `_index.md`:

```yaml
# content/pockist/_index.md
---
title: "Pockist"
weight: 10
---

# content/javascript/_index.md
---
title: "JavaScript"
weight: 20
---
```

Pockist will appear before JavaScript on the homepage.

### Control page order inside a section

Add `weight` to individual pages:

```yaml
---
title: "Dialog Service"
weight: 10
---
```

This also controls the order in the sidebar and on the section index page.

---

## Building for Production

```bash
hugo
```

This generates the static site into the `public/` directory. Deploy the contents of `public/` to any static host (GitHub Pages, Netlify, Vercel, S3, etc.).

---

## Deploying with rsync

`rsync` is the fastest way to deploy to a remote server — it only transfers changed files and can delete old ones automatically.

### Basic command

```bash
hugo --gc --minify
rsync -avz --delete public/ user@your-server.com:/var/www/html/
```

### Common flags

| Flag | What it does |
|------|-------------|
| `-a` | Archive mode (preserves permissions, timestamps, recursive) |
| `-v` | Verbose — shows which files are transferring |
| `-z` | Compress during transfer (faster on slow networks) |
| `--delete` | **Crucial** — removes files on the server that no longer exist in `public/` |
| `--dry-run` | Preview what *would* happen without actually doing it (test first!) |

### Example deploy script

Create `deploy.sh` in the project root:

```bash
#!/bin/bash
set -e

echo "Building site..."
hugo --gc --minify

echo "Deploying to server..."
rsync -avz --delete public/ user@your-server.com:/var/www/html/

echo "Done!"
```

Make it executable and run it:

```bash
chmod +x deploy.sh
./deploy.sh
```

---

## Project Structure

```
my-docs/
├── content/                       # All markdown content
│   ├── _index.md                  # Homepage intro (must be named _index.md)
│   ├── chats/
│   │   ├── _index.md              # Section intro & title for "Chats"
│   │   └── chat.md                # Page inside section
│   ├── javascript/
│   │   ├── _index.md              # Section intro & title for "JavaScript"
│   │   └── js-snippets.md         # Page inside section
│   └── (add more folders here)
├── layouts/
│   ├── index.html                 # Custom homepage layout (grouped by section)
│   └── _default/
│       └── section.html           # Section index page layout
├── assets/
│   └── _custom.scss               # Custom styles (darker background, etc.)
├── themes/
│   └── hugo-book/                 # Git submodule — docs theme
├── hugo.toml                      # Site config (dark mode, monokai, search, etc.)
└── README.md                      # This file
```

---

## Theme & Styling

- **Theme:** [Hugo Book](https://github.com/alex-shpak/hugo-book) (v9, dark mode)
- **Background:** Custom `#121212` via `assets/_custom.scss`
- **Syntax highlighting:** Chroma with `monokai` style
- **Search:** Built-in Flexsearch, enabled
- **Sidebar:** Auto-generated from all content in `content/`
- **Table of contents:** Enabled on every page
- **Homepage:** Grouped by section with links to section index pages
- **Section pages:** Auto-generated at `/folder-name/` listing pages inside

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



## Symlink the README into Content

If you want the root `README.md` to also appear as a page on the site (e.g., at `/readme/`), you can symlink it into `content/` instead of copying:

```bash
rm content/README.md  # remove existing copy if present
ln -s $(pwd)/README.md $(pwd)/content/README.md
```

Hugo follows symlinks, so any edits to the root `README.md` are automatically reflected in the build. No more manual copying.

**Note:** If the README doesn't have front matter, Hugo will derive the title from the filename ("Readme"). Add this to the top of `README.md` to set a custom title:

```markdown
---
title: "My Docs"
---

# My Docs
...
```

