---
name: readme-html-converter
description: Convert README.md or other Markdown technical documentation into a standalone interactive README.html while preserving all source information. Use when the user asks to turn README/readme/Markdown docs into HTML with hierarchical sections, page-like navigation, tabs, labels, copy buttons, configuration parameter previews, or interactive documentation UI. 适用于把技术文档从 Markdown 改成分区分层的 HTML，并加入参数演示、一键复制、分页和标签式阅读体验。
---

# README HTML Converter

## Goal

Create a polished `README.html` from `README.md` or another Markdown technical document. Preserve every piece of source information, then reorganize it into a clearer interactive document with hierarchy, tabs, page sections, copy actions, and configuration previews.

## Default Output

- Write `README.html` next to the source README unless the user gives another destination.
- Make the HTML standalone: inline CSS and vanilla JavaScript by default, with no CDN dependency.
- Keep the original Markdown file unchanged unless the user explicitly asks to edit it.
- Use ASCII unless the source document or required visible Chinese text already uses non-ASCII.
- Prefer semantic HTML: `header`, `nav`, `main`, `section`, `article`, `table`, `code`, `pre`.

## Workflow

1. Read the full source Markdown before editing.
2. Build an information inventory:
   - headings and hierarchy
   - paragraphs and notes
   - lists and checklists
   - tables
   - code blocks and commands
   - environment variables, config keys, ports, URLs, credentials placeholders
   - screenshots, image links, badges, external links
   - install, run, deploy, troubleshooting, FAQ, license, contribution sections
3. Create a content map that keeps all source information but improves navigation:
   - top-level tabs for major document areas
   - page-like sections inside long tabs
   - side table of contents for quick jumps
   - tags for content type, such as `Install`, `Config`, `API`, `Deploy`, `Troubleshooting`
4. Implement `README.html` using the template pattern in `assets/readme-html-template.html` when useful.
5. Add interaction for real user tasks, not decoration:
   - copy buttons for commands, code blocks, env examples, URLs, JSON payloads, and important parameters
   - tabs for major areas
   - pagination or step navigation for long flows
   - collapsible advanced details
   - search/filter for dense docs when helpful
   - parameter preview panels for configurable systems
6. Verify no source content was lost.

## Content Preservation Rules

- Do not summarize away information from the README.
- Do not replace specific commands, paths, env names, ports, or API fields with generic wording.
- If a section is awkward, preserve the text and wrap it in a better UI block instead of deleting it.
- Keep all links and images. If an image path is relative, keep the same relative path unless the HTML output location changes.
- Preserve code block languages where known, such as `bash`, `json`, `ts`, `js`, `python`, `sql`, or `yaml`.
- If Markdown contains badges or raw HTML, carry them into the generated document or recreate the same visible information.

## Layout Requirements

Use a document-app layout, not a marketing landing page:

- Top bar: document title, short source-derived subtitle, search if useful.
- Left or sticky navigation: generated from headings.
- Main area: tabbed major sections.
- Page controls: split long installation/deployment/usage flows into steps or pages.
- Tags: small labels that describe section type or importance.
- Utility strip: copy all relevant commands/config snippets.
- Responsive design: mobile should collapse navigation into a compact menu or horizontal tab row.

Keep visual styling restrained and technical:

- Avoid decorative hero sections, gradient-heavy backgrounds, and purely ornamental art.
- Use readable code blocks with strong contrast.
- Use cards only for repeated items, parameter demos, copied snippets, or warnings; do not nest cards inside cards.
- Keep radius at `8px` or less unless the surrounding project already uses another system.

## Interactive Parameter Demos

When the README describes system parameters, environment variables, CLI flags, API request bodies, ports, feature toggles, deployment targets, or account settings, add a small interactive preview.

The preview should:

- choose 3-8 representative parameters, not every possible field if the list is huge
- use controls that match the data type:
  - boolean -> toggle/checkbox
  - enum -> segmented control or select
  - number -> input, slider, or stepper
  - string/path/url -> text input
  - secret -> password-like field with placeholder, not real secret
- render the resulting config, command, `.env`, JSON, or URL preview live
- include copy buttons for the generated preview
- clearly mark demo values as examples when they are not production defaults

Example interaction targets:

- `.env` preview after setting `PORT`, `DATABASE_URL`, `JWT_SECRET`, and feature toggles
- `npm run dev -- --port 3000` command preview after changing a port
- API request JSON preview after choosing role, limit, or mode
- Docker command preview after choosing image tag and exposed port

## Conversion Heuristics

- Map README headings to tabs by meaning, not just heading level:
  - overview/introduction/features -> `Overview`
  - installation/quick start/setup -> `Setup`
  - usage/examples/workflow -> `Usage`
  - environment/config/options -> `Config`
  - API/endpoints/schema -> `API`
  - deployment/docker/production -> `Deploy`
  - troubleshooting/FAQ/common issues -> `Help`
- If the README is short, keep tabs but avoid excessive pagination.
- If the README is long, add per-tab page controls so users can move through sections without endless scrolling.
- Tables should remain tables, with horizontal scroll on mobile.
- Long code blocks should have copy buttons and preserve line breaks.
- Commands should be visually distinct from configuration files.

## Verification Checklist

Read `references/conversion-checklist.md` when doing a substantial conversion or when the README is long. At minimum, verify:

- every source heading appears in `README.html` or has an equivalent visible label
- every source code block appears with copy support
- every table appears with the same rows and columns
- every link target is preserved
- every config key/env var/CLI flag/API field is preserved
- parameter demos use values derived from the README or clearly marked examples
- the HTML works by opening it directly in a browser
- mobile width does not hide essential navigation or overflow text

## When Source README Is Missing

If no README exists in the target directory, do not invent project documentation. Tell the user the source file is missing and offer to create a skill/template-only artifact or to generate README content from the repo after inspection.
