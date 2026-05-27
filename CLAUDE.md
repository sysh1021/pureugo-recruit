# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository contains a **single static HTML landing page** (`index.html`) — a Korean-language recruitment page for 푸르고 (Purugo) 제3기 팀장 모집 (3rd cohort team leader recruitment), targeting married couples (부부팀) for a cleaning service business.

There is no build system, no dependencies, no test suite, and no JavaScript. The entire page is a single self-contained HTML file with inline `<style>` CSS.

## Development Workflow

- **Preview locally**: open `index.html` directly in a browser, or serve the directory with any static server (e.g. `python3 -m http.server 8000`). There is no build step.
- **Deploy**: the file is named `index.html` (renamed from `3기 모집공고.html` in commit `b7550fb`), which is the conventional entry point for static hosts like GitHub Pages — assume any push to `main` is potentially user-visible.
- **No lint/test commands exist.** Validate changes by visually inspecting in a browser at both desktop and mobile widths (the responsive breakpoint is `max-width: 600px`).

## Architecture & Conventions

### Single-file structure
All markup, styles, and content live in `index.html`. CSS is defined once in a `<style>` block at the top; the `<body>` is composed of a stack of section cards inside `.container` (max-width 680px, mobile-first).

### Section card system
The page is built from reusable section "cards" with a small set of background variants. When adding a new section, reuse these classes rather than introducing new color tokens:

- `.section` — base card (padding, rounded corners, shadow)
- Light variants: `.section-light` (indigo tint), `.section-white`, `.section-cream` (yellow tint), `.section-mint` (green tint)
- Bold gradient variants: `.section-dark` (indigo→purple), `.section-gold` (amber), `.section-green` (emerald), `.section-purple` (violet)
- Special blocks: `.accent-box` (indigo gradient inset), `.gold-box` (amber inset), `.promise` (dark indigo CTA), `.footer-cta` (green CTA with `.btn`)

Gradient sections override heading color via the `.section-dark h2` / `.section-gold h2` / etc. pattern — preserve this when adding new gradient variants.

### Layout primitives
- `.grid` + `.grid-2` / `.grid-3` for card grids (both collapse to 1 column under 600px)
- `.card` for the standard white tile with emoji + h3 + p
- `.faq-item` for Q&A blocks (left border accent)
- `.tag-item` for pill-shaped requirement tags

### Color palette
The design uses a consistent indigo/violet primary (`#4338ca`, `#4f46e5`, `#6d28d9`, `#312e81`) with amber/gold accents (`#fbbf24`, `#f59e0b`) and emerald (`#059669`, `#047857`) for the final CTA. Avoid introducing new hues — pick from these families.

### Content conventions
- All copy is **Korean**. Preserve Korean punctuation (`·`, `—`) and emoji-prefixed headings (e.g. `💡 왜 푸르고인가요?`).
- The primary CTA is the Google Form link in the `#apply` footer section (`https://forms.gle/zoTuJnguxsVYFbGn8`). When asked to change the application target, update this href.
- The cohort number ("제3기", "3기") appears in many places — when bumping cohorts, search/replace carefully across headings, badges, FAQ, and the footer.

## Git Workflow

The repo has two branches of interest: `main` (deploy target) and the active working branch. The remote is `sysh1021/pureugo-recruit`. History is shallow (2 commits as of this writing) — keep commits focused and descriptive since each one is significant relative to repo size.
