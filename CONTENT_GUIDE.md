# Content Guide

This is the only file you need to edit the site's content. No HTML or
CSS knowledge required — just plain text files.

**Rule of thumb:** if you're changing words, a link, or which image/video
shows up, you're editing a file in `_data/` or `_projects/`. You should
never need to open `_layouts/`, `_includes/`, or `assets/css/`.

After editing any file below, if you're running the site locally
(`bundle exec jekyll serve`), just save the file — the page updates
automatically in your browser within a second or two. (Exception: if
you ever edit `_config.yml`, you need to stop and restart the server.)

---

## 1. Edit the Home page

File: [`_data/home.yml`](_data/home.yml)

Open it and change any of these values (keep the quotes):

```yaml
name: "Your Name"
tagline: "Postdoctoral Researcher in [Your Field], [Your Institution]"

bio: >
  A couple of sentences about yourself go here.

photo: "profile-placeholder.svg"

background:
  image: "home-background-placeholder.svg"
  opacity: 0.18

links:
  - label: "Email"
    url: "mailto:you@example.com"
  - label: "Google Scholar"
    url: "https://scholar.google.com/citations?user=XXXXXXX"
```

- **`bio`** — plain text, or basic Markdown like `**bold**` or `[a link](https://example.com)`.
- **`photo`** — just the filename. The actual image file goes in `assets/images/` (see §3 below).
- **`background.opacity`** — a number from `0` (background image invisible) to `1` (fully solid). Try `0.4` for something more visible.
- **`links`** — add, delete, or reorder entries freely. Each one just needs a `label` (the text shown) and a `url`. For an email link, use `"mailto:you@example.com"`.

---

## 2. Add or remove a Research project

Each project is one file in [`_projects/`](_projects/). To see a full
working example, open [`_projects/example-project.md`](_projects/example-project.md).

**To add a new project:** copy `_projects/example-project.md`, rename the
copy (e.g. `_projects/protein-folding-sim.md` — the filename doesn't
appear anywhere on the site, so name it whatever helps *you* find it
later), then edit the copy:

```yaml
---
title: "Example Research Project"
image: "project-example-placeholder.svg"
order: 1
collaborators:
  - name: "Jane Doe"
    url: "https://example.com/jane-doe"
  - name: "John Smith"
    url: "https://example.com/john-smith"
---

Description of the project goes here, as regular text/Markdown. Write
as many paragraphs as you like — this becomes the card's description.
```

- **`title`** — the project name shown on the card.
- **`image`** — filename of the thumbnail image, placed in `assets/images/` (see §3).
- **`image_width`** — optional. A number from `1` to `100`, the percentage of the card's width the image should take up (it's centered, and scaled proportionally — the aspect ratio never changes). Leave it out for full width (100).
- **`order`** — a number controlling display order on the page (lower = higher up). Leave it out and it defaults to `0`.
- **`collaborators`** — a list of people. Each needs a `name`; `url` is optional — if you omit `url`, the name just shows as plain text instead of a link.
- Everything below the second `---` is the description text.

**To remove a project:** delete its file from `_projects/`. That's it.

**To link to the published paper(s)** (optional — omit entirely if there's no publication yet), add this to the front matter:
```yaml
publications:
  - label: "Read the paper"
    url: "https://doi.org/xxxxx"
```
`label` is optional — leave it out and it defaults to "Read the paper". `url` can be a DOI, arXiv link, or journal page.

Add more than one by adding another `- label / url` entry underneath — useful when a project has a paper *and* a companion tool/dataset, for example:
```yaml
publications:
  - label: "Read the paper"
    url: "https://doi.org/xxxxx"
  - label: "Explore the interactive dataset"
    url: "https://example.com/my-project-tool"
```

⚠️ Each entry needs its own `- label / url` pair under the same `publications:` list — don't repeat the `publications:` key itself for a second entry (YAML silently keeps only the last one if you do, dropping earlier links without any error).

**To add a video to a project** (optional — omit entirely for no video), add one of these two blocks to the front matter:

*A YouTube video:*
```yaml
video:
  type: youtube
  id: "YOUR_YOUTUBE_VIDEO_ID"
```
The ID is the part after `watch?v=` in a YouTube URL (e.g. for `youtube.com/watch?v=abc123XYZ`, the ID is `abc123XYZ`).

*A local video file* (e.g. a short simulation clip), useful when you don't want to rely on YouTube:
```yaml
video:
  type: local
  file: "my-simulation.mp4"
```
Place the `.mp4` file in `assets/videos/` (see §3). Keep local videos short/compressed — large files bloat the repository and slow down page loads.

---

## 3. Swap or add an image / video

Every image lives in [`assets/images/`](assets/images/); every video lives in [`assets/videos/`](assets/videos/).

To use a new file:
1. Drop the file into the right folder (e.g. `assets/images/my-photo.jpg`).
2. Reference it **by filename only** (not the full path) in the relevant data file — e.g. `photo: "my-photo.jpg"` in `_data/home.yml`, or `image: "my-photo.jpg"` in a project's front matter.

Any common image format works (`.jpg`, `.png`, `.svg`, `.webp`). For video, use `.mp4` for the widest browser support.

---

## 4. Add or remove a Publication

File: [`_data/publications.yml`](_data/publications.yml)

This is a single list — every publication is one entry, indented the same way. To add one, copy an existing entry (including the leading `-`) and edit it:

```yaml
- title: "An Example Publication Title Goes Here"
  authors: "Jane Doe, John Smith, Your Name"
  venue: "Journal of Examples"
  year: 2026
  links:
    - label: "PDF"
      url: "https://example.com/example-paper.pdf"
    - label: "DOI"
      url: "https://doi.org/10.xxxx/example"
    - label: "arXiv"
      url: "https://arxiv.org/abs/xxxx.xxxxx"
```

- **`authors`** — just plain text, written however you'd like it displayed (e.g. bold your own name if you want — `"Jane Doe, **Your Name**"` — Markdown isn't applied here, so bolding won't render, but you can order/format the names as plain text).
- **`year`** — publications are automatically sorted newest-first on the page, so you never need to manually order this file.
- **`links`** — same `label`/`url` pattern as everywhere else on the site. Add as many or as few as you want (PDF, DOI, arXiv, journal page, etc.) — each just needs a `label` (the text shown) and a `url`. Omit the whole `links:` block if there's nothing to link to yet.

**To remove a publication:** delete its entry (the `-` line and everything indented under it) from the file.

**To mark something as a preprint** instead of a finished publication, add `type: preprint` to that entry. It will then show up under the "Preprints" heading on the page instead of "Publications" — no other changes needed. Leave `type` out entirely for a normal, published entry.

---

## 5. Edit the Contact page

File: [`_data/contact.yml`](_data/contact.yml)

```yaml
email: "you@example.com"

affiliations:
  - institution: "Your Institution"
    address: |
      Department of Example Studies
      Example University
      123 Example Street
      City, Postal Code, Country

  - institution: "Second Institution"
    address: |
      Department Name
      Second Institution
      456 Example Avenue
      City, Postal Code, Country

links:
  - label: "Google Scholar"
    url: "https://scholar.google.com/citations?user=XXXXXXX"
  - label: "ORCID"
    url: "https://orcid.org/0000-0000-0000-0000"
```

- **`email`** — shown as a clickable `mailto:` link automatically, as long as the value contains an `@`. If you'd rather not expose a real address to spam bots, write it in an obfuscated, human-readable form without an `@` (e.g. `"you [at] example [dot] com"`) — it'll then just display as plain text instead of a link.
- **`affiliations`** — a list; add, remove, or reorder entries freely. Each one has its own `institution` name and `address`, so you can list two (or more) affiliations, each with its own address. If you only have one, just delete the second entry.
- **`address`** — keep the `|` on its own line exactly as shown, then indent every address line under it (matching the indentation of the `institution:` line above it). Each line you write becomes its own line on the page (no need for HTML `<br>` tags).
- **`links`** — same `label`/`url` pattern used everywhere else on the site.
- To hide any of these sections entirely, just delete that field (or its value) from the file.
