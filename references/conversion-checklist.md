# README to HTML Conversion Checklist

Use this checklist before finishing an interactive `README.html`.

## Source Inventory

- Record all headings in order.
- Count all fenced code blocks and note their languages.
- Record all tables and row counts.
- Record all links, image paths, badges, and raw HTML snippets.
- Record all commands, env vars, config keys, ports, hostnames, URLs, API routes, request fields, and response fields.
- Record warnings, notes, limitations, TODOs, and troubleshooting items.

## HTML Structure

- Use one document shell with a sticky or clearly available navigation area.
- Group content into top-level tabs based on task category.
- Keep source heading order inside each tab unless there is a strong reason to reorder.
- Use page or step controls for long setup/deploy/use flows.
- Add tags that help scanning, such as `Required`, `Optional`, `Local`, `Production`, `API`, `Example`, `Warning`.
- Keep tables responsive with an overflow wrapper.
- Keep code blocks readable and copyable.

## Interaction

- Copy button on each command/code/config block.
- Live preview for representative parameters when the README includes configurable values.
- Tabs should update active state and show exactly one tab panel at a time.
- Page controls should not hide content permanently; all pages must be reachable.
- Search/filter should hide only matching content temporarily and be easy to clear.
- Interactive demos must not require external services.

## Parameter Demo Quality

- Use realistic parameter names from the README.
- Use safe placeholders for secrets.
- Mark generated config as an example if values are invented.
- Generate a useful final artifact: `.env`, JSON, command, URL, YAML, or Docker command.
- Include a copy button for the generated artifact.

## Final Verification

- Compare generated navigation against source headings.
- Compare code block count against source inventory.
- Compare table count and important rows against source inventory.
- Click every top-level tab and every page control.
- Test at least one copy button.
- Change every parameter demo control and confirm the preview updates.
- Open the HTML directly from disk or through the project dev server.
- Check a narrow viewport for text overflow and hidden controls.
