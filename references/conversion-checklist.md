# README to HTML Conversion Checklist

Use this checklist before finishing an interactive `README.html`.

## Source Inventory

- Record the important project tree before converting: source folders, app/server entrypoints, config folders, scripts, deployment files, tests, docs, and static assets.
- Record key manifest/config files when present: `package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `Dockerfile`, `docker-compose*.yml`, `.env.example`, framework configs, and CI files.
- Record all headings in order.
- Count all fenced code blocks and note their languages.
- Record all tables and row counts.
- Record all links, image paths, badges, and raw HTML snippets.
- Record all commands, env vars, config keys, ports, hostnames, URLs, API routes, request fields, and response fields.
- Record warnings, notes, limitations, TODOs, and troubleshooting items.
- Record README claims that appear stale or inconsistent with actual project files.
- Record the source for important facts: README, manifest/config file, observed file tree, or inference.
- Record sensitive keys without recording real sensitive values.

## HTML Structure

- Use one document shell with a sticky or clearly available navigation area.
- Group content into top-level tabs based on task category.
- Keep source heading order inside each tab unless there is a strong reason to reorder.
- Use page or step controls for long setup/deploy/use flows.
- Add tags that help scanning, such as `Required`, `Optional`, `Local`, `Production`, `API`, `Example`, `Warning`.
- Include a project structure or architecture section when the repository contains meaningful code/config/deployment/test files beyond the README.
- Include source labels or source notes for commands, config values, entrypoints, deployment facts, and project structure summaries.
- Include a scan summary that lists detected stack, scripts, entrypoints, config files, deployment files, and tests when available.
- Surface README-vs-project conflicts in a visible warning block.
- Keep tables responsive with an overflow wrapper.
- Keep code blocks readable and copyable.
- If navigation links point into tabbed, paged, collapsed, or otherwise hidden content, add JavaScript that reveals the containing UI before scrolling.
- Support initial hash URLs such as `README.html#deploy` by activating the correct tab/page on load.
- Produce one self-contained HTML file only. Inline CSS and JavaScript in `README.html`; do not create extra `.html`, `.css`, `.js`, preview, template, or asset files unless explicitly requested.

## Interaction

- Copy button on each command/code/config block.
- Live preview for representative parameters when the README includes configurable values.
- Tabs should update active state and show exactly one tab panel at a time.
- Page controls should not hide content permanently; all pages must be reachable.
- Search/filter should hide only matching content temporarily and be easy to clear.
- Interactive demos must not require external services.
- Controls should be keyboard reachable and have visible active/focus states.
- Copy actions should show success/failure feedback.

## Parameter Demo Quality

- Use realistic parameter names from the README.
- Use safe placeholders for secrets.
- Never show real secret values from `.env`, production configs, key files, tokens, cookies, database URLs, or private credentials.
- Mark generated config as an example if values are invented.
- Generate a useful final artifact: `.env`, JSON, command, URL, YAML, or Docker command.
- Include a copy button for the generated artifact.

## Final Verification

- Compare generated navigation against source headings.
- Confirm the project structure scan is reflected in the HTML when relevant.
- Confirm actual scripts, entrypoints, env examples, and deployment files are not contradicted by the generated instructions.
- Confirm important facts include source labels or clear source wording.
- Confirm README-vs-project conflicts are visible and not silently resolved.
- Confirm real secrets and credentials are not present in the HTML or copy targets.
- Compare code block count against source inventory.
- Compare table count and important rows against source inventory.
- Click every top-level tab and every page control.
- Click every sidebar/table-of-contents link, especially links to sections inside inactive tabs or pages.
- Open at least one hash deep link directly and confirm the right tab/page becomes visible.
- Test at least one copy button.
- Change every parameter demo control and confirm the preview updates.
- Navigate interactive controls by keyboard at least once.
- Open the HTML directly from disk or through the project dev server.
- Confirm the conversion did not create any companion output files beside the single requested HTML file.
- Check a narrow viewport for text overflow and hidden controls.
