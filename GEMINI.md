# GEMINI.md — Zeus Sport Shopify Theme (Dawn)

## Project Overview

This repository is a customized **Shopify Dawn theme** for **Zeus Sport**, a premium sports apparel brand and official FC Crotone merchandise partner. The theme is built on top of Shopify's open-source Dawn theme and extended with brand-specific sections, styles, and components.

---

## Repository Structure

```
zeuscalabria/
├── .agents/
│   ├── references/       # Visual design references (screenshots of target UI)
│   ├── skills/           # Agent skill definitions (see Skills section)
│   └── tasks/            # Scoped development tasks (e.g. task_1.md)
├── assets/               # CSS, JS, image assets (Shopify convention)
├── config/               # Theme settings schema (settings_schema.json, settings_data.json)
├── layout/               # Theme layout files (theme.liquid)
├── locales/              # Translation strings
├── sections/             # Shopify sections (.liquid files)
├── snippets/             # Reusable Liquid snippets
├── templates/            # Page/product/collection templates
├── .gitignore
├── .prettierrc.json
├── .theme-check.yml
├── skills-lock.json
├── translation.yml
└── GEMINI.md             # This file
```

---

## Agent Instructions

You are an AI coding agent working on a Shopify Dawn theme. Your job is to implement frontend UI tasks by writing clean, production-grade Liquid, CSS, and JavaScript following Shopify best practices.

### How to Work

1. **Read the task file** in `.agents/tasks/` to understand what needs to be implemented.
2. **Consult the references** in `.agents/references/` — these are visual mockups (PNG screenshots) showing the desired output. Treat them as the source of truth for layout, spacing, and visual design.
3. **Apply the relevant skills** from `.agents/skills/` before writing any code:
   - `shopify-expert`: Shopify Liquid conventions, section schema, metafields, Online Store 2.0 patterns.
   - `frontend-design`: Visual design quality, typography, color, motion, spatial composition.
   - `web-design-guidelines`: Accessibility, responsive design, performance standards.
4. **Write the code** following the patterns described below.
5. **Do not modify** files outside the scope defined in the task.

---

## Coding Standards

### Shopify / Liquid

- Follow **Online Store 2.0** section architecture: every section must have a `{% schema %}` block with `name`, `settings`, and `presets`.
- Use **section settings** for any value that a merchant might want to customize (colors, text, images, toggle options).
- Use `{{ section.settings.* }}` to reference schema values — never hardcode content that belongs in settings.
- Use `{{ 'file.css' | asset_url | stylesheet_tag }}` and `{{ 'file.js' | asset_url | script_tag }}` for asset loading.
- Images must use `{{ image | image_url: width: N | image_tag: loading: 'lazy', ... }}` — never use raw `<img src>` with Liquid URLs.
- For responsive images use the `widths` filter with appropriate breakpoints.
- Use `{{ 'key' | t }}` for all user-facing strings; add translations to `locales/`.
- Prefix custom CSS classes with a section-specific namespace (e.g. `.zeus-categories__card`) to avoid Dawn conflicts.
- Do **not** override Dawn's base CSS variables (`--color-base-*`, `--font-body-*`) unless explicitly required by the task. Add new variables instead.

### CSS

- Write scoped CSS inside `assets/section-name.css` or inline in `<style>` within the section if the ruleset is small (<50 lines).
- Use CSS custom properties for all colors, gradients, and spacing values defined by the design.
- Mobile-first: base styles target mobile, use `@media (min-width: 750px)` and `@media (min-width: 990px)` for tablet/desktop overrides (Dawn breakpoints).
- Prefer CSS Grid and Flexbox. Do not use floats.
- Animations must respect `@media (prefers-reduced-motion: reduce)`.

### JavaScript

- Use vanilla JS or Dawn's existing utilities. Do not introduce new npm dependencies unless the task explicitly permits it.
- Scripts must be deferred: `<script src="..." defer></script>`.
- No inline `onclick` attributes — use `addEventListener`.

### Accessibility

- All interactive elements must be keyboard-navigable and have visible focus styles.
- Images must have meaningful `alt` text (pulled from section settings or product data).
- Color contrast must meet WCAG AA (4.5:1 for normal text, 3:1 for large text).
- Use semantic HTML: `<section>`, `<article>`, `<nav>`, `<h2>` hierarchy, etc.

---

## Visual References

The `.agents/references/` folder contains the following design mockups to use as ground truth:

| File | Description |
|---|---|
| `homepage.png` | Full desktop homepage layout |
| `homepage-mobile.png` | Mobile homepage layout |
| `plp.png` | Product Listing Page (collection page) |
| `pdp.png` | Product Detail Page |
| `category-chips.png` | Category section chip/card component detail |

Always open and study the relevant reference images before implementing any section or component.

---

## Skills Reference

Before writing code, read and apply the skill definitions located in `.agents/skills/`:

### `shopify-expert`
Provides patterns for: section schema authoring, metafield usage, Liquid best practices, Dawn theme conventions, Shopify CLI workflows, and theme check compliance.

### `frontend-design`
Guides visual decision-making: typography pairing, color systems, motion design, spatial composition, and avoiding generic/low-quality UI patterns. Apply this to ensure the output matches the premium aesthetic of the Zeus Sport brand.

### `web-design-guidelines`
Covers: responsive layout principles, accessibility standards, performance (lazy loading, asset optimization), and cross-browser compatibility.

---

## Tasks

Development tasks are defined as Markdown files in `.agents/tasks/`. Each task file contains:
- A problem statement and objectives
- Scope (which files to touch)
- Specific requirements and design constraints

### Current Tasks

| File | Title | Status |
|---|---|---|
| `task_1.md` | Zeus Sport Homepage — Category Section Enhancement | ✅ Approved for Development |

**task_1.md Summary:**
Enhance the "Categories" section on the desktop homepage by replacing placeholder imagery with authentic product/athlete photography. The section contains 5 cards (Uomo, Donna, Bambino, FC Crotone, Accessori), each requiring a specific real image, colored gradient overlay, and bold white category title. Visual reference: `homepage.png` and `category-chips.png`.

---

## Theme Check

This repo uses `.theme-check.yml` for Shopify Theme Check linting. Before committing:

```bash
shopify theme check
```

All errors must be resolved. Warnings should be reviewed and addressed unless explicitly documented as acceptable.

---

## Formatting

Code formatting is enforced via `.prettierrc.json`. Run before committing:

```bash
prettier --write "**/*.{css,js,json}"
```

Liquid files are formatted following Shopify's Liquid Prettier plugin conventions.

---

## Notes for the Agent

- The base theme is **Dawn**. When in doubt about a pattern, refer to how Dawn implements similar sections (e.g. `sections/featured-collection.liquid`, `sections/image-banner.liquid`).
- Zeus Sport's brand identity is **premium, sporty, and authentic**. Avoid generic or placeholder aesthetics.
- The FC Crotone partnership is a key brand differentiator — treat it with visual prominence.
- Always validate that new sections appear correctly in the **Shopify Theme Editor** (i.e. schema presets are defined and settings are labeled clearly in Italian/English as appropriate).