# tinamkemp.com — site source

A small static site built with [Eleventy](https://www.11ty.dev/), styled with the
Tina M. Kemp brand kit (slate blue / Cormorant Garamond + Jost).

## Summary

- A static personal site for tinamkemp.com, built with Eleventy (11ty) — no database, no CMS, no server code; Markdown files compile straight to HTML.
- Entry point: `.eleventy.js` is the build config — it sets `src/` as input, `_site/` as output, defines the `posts` collection, the `readableDate` filter, and the `currentYear` global.
- Homepage source: `src/index.md`, rendered through the shared layout `src/_includes/base.njk` (header/nav/footer shell).
- Content model: each route is a Markdown file with YAML front matter (`src/about/index.md`, `src/contact/index.md`, `src/consulting/index.md`), plus an intended `src/posts/*.md` + `src/writing/index.md` writing section (currently missing from source, though old built output for it still sits in `_site/`).
- Output/deploy: `npx @11ty/eleventy` builds everything into `_site/`, which is manually uploaded via SFTP to DreamHost — no CI/CD.

## What this is

- No database, no CMS, no subscription fees.
- Plain Markdown files become HTML pages.
- New "Writing" posts are added by dropping a `.md` file into `src/posts/` —
  no HTML editing required.

## Folder structure

```
src/
  _includes/       — page templates (base.njk, post.njk)
  css/             — stylesheet (style.css)
  posts/           — writing entries, one .md file per post
  index.md         — homepage
  about/index.md   — About page
  writing/index.md — Writing index (auto-lists posts)
  contact/index.md — Contact page
  consulting/index.md — Consulting page (linked from About, not in nav)
.eleventy.js       — Eleventy configuration
```

## Local setup (one-time)

You'll need [Node.js](https://nodejs.org/) installed (the LTS version is fine).

```
npm install
```

## Building the site

```
npx @11ty/eleventy
```

This generates the finished site into a `_site/` folder. That `_site/` folder
is what you upload to DreamHost.

To preview locally while editing, run:

```
npx @11ty/eleventy --serve
```

This starts a local server (usually at `http://localhost:8080`) and rebuilds
automatically when you save a file.

## Adding a new "Writing" post

1. Copy `src/posts/a-first-entry.md` as a starting template (or create a new
   file in `src/posts/`).
2. Give the file a short, URL-friendly name, e.g. `src/posts/on-formation.md`.
3. Edit the front matter at the top of the file:

   ```
   ---
   layout: post.njk
   title: On Formation
   date: 2026-07-01
   excerpt: A one-sentence summary shown on the Writing index page.
   ---
   ```

4. Write the post body below the `---` line using Markdown.
5. Rebuild the site (`npx @11ty/eleventy`) — the new post appears automatically
   on the Writing page, sorted by date (newest first).

## Editing existing pages

Each page is a Markdown file with a little HTML mixed in for layout elements
(like the "callout" boxes). Edit the text between the front matter (`---`
lines) and the rest of the file is left alone.

- `src/index.md` — homepage
- `src/about/index.md` — About
- `src/writing/index.md` — Writing index (intro text only — posts are listed automatically)
- `src/contact/index.md` — Contact
- `src/consulting/index.md` — Consulting (not in main nav, linked from About)

## Deploying to DreamHost

1. Run `npx @11ty/eleventy` to generate the `_site/` folder.
2. Connect to your DreamHost server via SFTP (DreamHost panel → "SFTP Users" for credentials).
3. Upload the **contents** of `_site/` (not the folder itself) into your
   domain's web directory (usually `tinamkemp.com/` or similar — check the
   DreamHost panel under "Manage Websites").
4. Visit tinamkemp.com to confirm it's live.

Each time you make changes: rebuild with `npx @11ty/eleventy`, then re-upload
the changed files from `_site/`.

## Brand reference (for future edits)

| Role | Hex |
|---|---|
| Primary (headings, links) | `#3A5A72` |
| Secondary (rules, dividers) | `#7A92A8` |
| Accent (backgrounds, borders) | `#B5CADA` |
| Page background | `#F4F6F8` |
| Body text | `#444444` |

- Display font: Cormorant Garamond (Light/Regular)
- Body font: Jost (Light)

These are defined as CSS variables at the top of `src/css/style.css` — change
them there to update the whole site at once.
