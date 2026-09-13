# My website

Static Astro site deployed to GitHub Pages.

## Run locally

Use Node.js 22 and pnpm 10.34.5.

```sh
pnpm install --frozen-lockfile
pnpm dev
```

Open http://localhost:4321/. Changes reload automatically.

## Edit the site

| What | Where |
| --- | --- |
| About text, contact badges, quote and portrait sizing | `src/pages/index.astro` |
| Portrait image | `public/images/prof_pic.webp` |
| Shared colors, navigation, spacing and footer | `src/layouts/Layout.astro` |
| Eye colors, Stochastic/Bayer dithering and gaze settings | `src/components/GazeEye.astro` |
| Publications | `src/data/publications.json` |
| Blog posts | `src/content/blog/*.md` |

Colors use `--bg`, `--ink`, `--muted`, `--accent` and `--line`. Edit both light and dark palettes. Portrait sizing has desktop and mobile rules.

### Blog posts and Updates

Each post needs YAML frontmatter with `title`, `description`, `date`, `added` and `draft`. Dates use `YYYY-MM-DD`; the filename becomes `/blog/<filename>/`.

- `date`: the post's publication date.
- `added`: when the item was first added publicly to this site. Leave it unchanged for ordinary edits.
- Write drafts in `src/content/blog/drafts/` with `draft: true`. This folder is Git-ignored; posts are visible in `pnpm dev` at `/blog/drafts/<filename>/`, but excluded from production.
- To publish, move the file into `src/content/blog/`, set `draft: false` and set `added` to the public addition date. Its public URL becomes `/blog/<filename>/`.

Ignored drafts have no Git backup; back them up privately. Do not force-add the draft folder or put private draft assets in `public/`. Ignoring a file does not remove copies already committed to Git history.

About's **Updates** list automatically combines the six latest publications and non-draft posts by `added` date when built. No separate list to maintain.

### Publications

Only include work cleared for public disclosure; omit confidential work from the repository entirely. Follow an existing JSON record, using a unique `id` and an `added` date. Submitted entries use `status: "Submitted"`, `year: null` and `venue: null`; do not disclose their target venues. Use `url: null` when no public paper link exists. Optional `github` and `huggingFace` URLs add platform-colored code/model badges below the title; omit them when unavailable.

Optional thumbnails go in `src/assets/publications/`. Set `image` to the exact filename and `imageAlt` to descriptive text, or empty for decorative images. Prefer optimized WebP at up to 260 px for the current thumbnail size; animated WebP is supported. PNG, JPG/JPEG and GIF also work. Missing images are omitted. Titles and thumbnails link to `url` in a new tab; without a URL they remain unlinked. Resource badges also open in a new tab.

## Build and deploy

```sh
pnpm build
pnpm preview
```

The production build is in `dist/`; drafts are excluded.

Set the repository's GitHub Pages source to **GitHub Actions**. Pushes to `main` build and deploy through `.github/workflows/deploy.yml`; pull requests build without deploying. The site URL is configured in `astro.config.mjs`.
