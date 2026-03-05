# Kena Tuitoek — Quantitative Research Portfolio

Personal portfolio site built with Jekyll (academicpages theme). Hosted on GitHub Pages.

## Structure

```
_portfolio/     ← Project write-ups (add .md files here)
_research/      ← Research articles / working papers
_pages/         ← Static pages (home, CV, portfolio listing, research listing)
_includes/      ← Layout partials
_layouts/       ← Page templates
_sass/          ← Stylesheets
assets/         ← CSS, JS, fonts
images/         ← Profile pic, favicons
files/          ← Downloadable files (CV PDF, etc.)
```

## Adding a new project

Create a new `.md` file in `_portfolio/` with this front matter:

```yaml
---
title: "Your Project Title"
excerpt: "One-sentence summary."
collection: portfolio
category_label: "ML / Finance"        # shown as a colored label
status: "Complete"                     # or "In Progress"
accent_color: "#5B8DEF"               # hex color for the card accent
tagline: "Short subtitle"
methods:
  - Method 1
  - Method 2
tools:
  - Python
  - pandas
tags:
  - tag1
  - tag2
---

Your full project write-up in Markdown here.
Include code blocks, tables, images, LaTeX math, etc.
```

The project will automatically appear on the Portfolio page and homepage.

## Adding a research article

Same approach — create a `.md` file in `_research/`:

```yaml
---
title: "Paper Title"
collection: research
paper_type: "Working Paper"
date: 2025-06-01
excerpt: "Abstract summary."
tags:
  - keyword1
  - keyword2
---
```

## Local development

```bash
bundle install
bundle exec jekyll serve -l
```
