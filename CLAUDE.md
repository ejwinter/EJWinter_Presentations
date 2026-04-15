# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Structure

A monorepo of [Slidev](https://sli.dev) presentations. Each presentation lives in its own subdirectory with an independent `package.json`. There is no root-level package.json or shared build system.

```
<presentation-name>/
  slides.md        # All slide content and frontmatter
  package.json     # Slidev dev/build/export scripts
  slides-export.pdf  # Generated PDF (committed)
```

## Commands

All commands must be run from within the presentation's subdirectory:

```bash
cd <presentation-folder>
npm install       # First time setup (Node 18+)
npm run dev       # Dev server with hot reload at http://localhost:3030
npm run build     # Build static site
npm run export    # Export to PDF (requires playwright-chromium)
```

## Adding a New Presentation

1. Create a new subdirectory at the repo root.
2. Add a `package.json` modeled after `Agents_Context/package.json` — set a unique `"name"` field.
3. Create `slides.md` with Slidev frontmatter (`title`, `info`) and slide content separated by `---`.
4. Add an entry to `README.md` under the Presentations section.

## Slide Authoring Notes

- Slides are separated by `---` in `slides.md`; layout variants (`layout: section`, `layout: center`) go in the separator block.
- Speaker notes go in `<!-- ... -->` HTML comments immediately after the slide content.
- Tailwind utility classes are available for inline layout (e.g., `grid grid-cols-2 gap-8`).
- The default Slidev theme (`@slidev/theme-default`) is used; no custom theme has been added.
