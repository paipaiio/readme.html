---
name: readme-html-converter
description: Convert README.md or other Markdown technical documentation plus the surrounding project structure into a standalone interactive README.html while preserving all source information. Use when the user asks to turn README/readme/Markdown docs into HTML with hierarchical sections, page-like navigation, tabs, labels, copy buttons, source attribution, conflict warnings, secret redaction, project structure summaries, configuration parameter previews, or interactive documentation UI. 适用于读取 README 与整个项目结构后，把技术文档从 Markdown 改成分区分层的单文件 HTML，并加入来源标记、冲突提示、敏感信息脱敏、参数演示、一键复制、分页和标签式阅读体验。
---

# README HTML Converter

## Goal

Create a polished `README.html` from `README.md` or another Markdown technical document plus the surrounding project structure. Preserve every piece of source information, verify it against actual project files, mark where facts came from, redact secrets, surface conflicts, then reorganize it into a clearer interactive document with hierarchy, tabs, page sections, copy actions, project structure summaries, and configuration previews.

## Default Output

- Write `README.html` next to the source README unless the user gives another destination.
- Produce exactly one standalone HTML file: inline CSS and vanilla JavaScript in `README.html`, with no extra `.html`, `.css`, `.js`, asset, preview, template, or companion output files unless the user explicitly asks for them.
- Keep the original Markdown file unchanged unless the user explicitly asks to edit it.
- Use ASCII unless the source document or required visible Chinese text already uses non-ASCII.
- Prefer semantic HTML: `header`, `nav`, `main`, `section`, `article`, `table`, `code`, `pre`.

## Workflow

1. Read the full source Markdown before editing.
2. Scan the project structure before designing the HTML:
   - use `rg --files` when available
   - ignore generated or dependency folders such as `.git`, `node_modules`, `dist`, `build`, `.next`, `coverage`, `vendor`, `.venv`, `venv`, `__pycache__`, and `DerivedData`
   - inspect key manifests and configs when present: `package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `pom.xml`, `build.gradle`, `Dockerfile`, `docker-compose.yml`, `Makefile`, `.env.example`, framework configs, route/app directories, tests, and deployment files
3. Build an information inventory:
   - headings and hierarchy
   - paragraphs and notes
   - lists and checklists
   - tables
   - code blocks and commands
   - environment variables, config keys, ports, URLs, credentials placeholders
   - screenshots, image links, badges, external links
   - install, run, deploy, troubleshooting, FAQ, license, contribution sections
   - observed project directories, entrypoints, run scripts, build scripts, tests, API/routes, env examples, deployment files, and static assets
4. Classify source attribution for important facts:
   - `README` for original documentation claims
   - manifest/config source names such as `package.json`, `Dockerfile`, `.env.example`, `go.mod`, `pyproject.toml`
   - `Observed` for file tree or route structure inferred from the repository
   - `Inferred` only when the conclusion is reasonable but not directly stated
5. Reconcile README content with project evidence:
   - use README as the primary source for user-facing intent
   - use project files to verify commands, scripts, entrypoints, environment variables, framework, and deployment details
   - if README and project evidence conflict, do not silently overwrite one with the other; preserve the README claim and add a clear note such as `README says ...; project files show ...`
   - do not invent behavior from file names alone; mark inferred structure as observed evidence
6. Redact sensitive information before it reaches the HTML:
   - prefer `.env.example`, `.env.sample`, and documented placeholders
   - never expose real `.env` secrets, private keys, tokens, cookies, API keys, database passwords, or production credentials
   - show variable names and safe placeholders such as `replace-with-a-secure-secret`
   - if a required config value is found only in a sensitive file, document the key name and note that the value was intentionally hidden
7. Create a content map that keeps all source information but improves navigation:
   - top-level tabs for major document areas
   - page-like sections inside long tabs
   - side table of contents for quick jumps
   - tags for content type, such as `Install`, `Config`, `API`, `Deploy`, `Troubleshooting`
   - a project structure or architecture section when the repo contains meaningful source/config/deploy/test files
   - a scan summary section that lists detected stack, entrypoints, scripts, config files, deployment files, and tests when available
8. Implement `README.html` as a single self-contained file with inline CSS and JavaScript.
9. Add interaction for real user tasks, not decoration:
   - copy buttons for commands, code blocks, env examples, URLs, JSON payloads, and important parameters
   - tabs for major areas
   - pagination or step navigation for long flows
   - collapsible advanced details
   - search/filter for dense docs when helpful
   - parameter preview panels for configurable systems
10. Verify no source content was lost and the generated page reflects both README content and relevant project structure.

## Project Structure Reading

Always inspect the actual project around the README unless the user explicitly asks for README-only conversion.

Prioritize these files and directories:

- manifest/package files: `package.json`, `pnpm-workspace.yaml`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `pom.xml`, `build.gradle`
- runtime entrypoints: `src/`, `app/`, `pages/`, `server/`, `main.*`, `index.*`, route files, CLI entry files
- configuration: `.env.example`, `.env.sample`, `config/`, `vite.config.*`, `next.config.*`, `tsconfig.json`, `tailwind.config.*`
- deployment: `Dockerfile`, `docker-compose*.yml`, `vercel.json`, `netlify.toml`, `nginx*.conf`, CI workflows
- tests and quality: `tests/`, `__tests__/`, `spec/`, lint/test scripts, coverage config
- existing docs: `docs/`, `CHANGELOG`, `CONTRIBUTING`, API docs

Use the scan to improve the HTML:

- add a scan summary with source badges for facts that came from the README or files
- add a project structure section with a concise tree of important paths
- add run/build/test/deploy command blocks from actual scripts when available
- add config and env panels from actual examples and config files
- add API/route summaries only when routes are visible or documented
- add warnings for missing files, stale README commands, or undocumented required setup

Keep the scan bounded:

- for large repositories, summarize important folders and inspect representative entry/config files instead of reading every source file
- prefer manifests, configs, routes, env examples, deployment files, tests, and docs over implementation internals
- do not scan generated, dependency, cache, binary, or build artifact folders
- keep the HTML focused on practical usage, setup, configuration, deployment, and architecture facts a user needs

## Source Attribution And Conflicts

Important facts in the HTML should show where they came from. Use small badges or labels such as:

- `README`
- `package.json`
- `.env.example`
- `Dockerfile`
- `Observed`
- `Inferred`

Use attribution for commands, scripts, config values, ports, entrypoints, deployment instructions, API routes, and project structure summaries.

When evidence conflicts:

- preserve the README claim
- show the project-file evidence next to it
- explain the risk plainly, for example: `README says npm start, but package.json does not define a start script`
- do not choose a winner unless the code/config evidence is definitive
- put conflicts in a visible warning block or a scan summary section

## Sensitive Data Safety

Never expose real secrets in `README.html`.

Treat these as sensitive by default:

- `.env`, `.env.local`, `.env.production`, `.npmrc`, `.pypirc`
- private keys, certificates, tokens, cookies, session secrets
- database URLs with credentials
- cloud provider keys and webhook secrets
- passwords and production host credentials

Safe behavior:

- read sensitive files only enough to discover required key names when necessary
- redact values immediately
- render placeholders instead of real values
- never add copy buttons that copy real secrets
- prefer sample files and documentation examples over live credential files

## Accessibility And Interaction Quality

Interactive HTML must remain usable:

- controls must be keyboard reachable
- active/focus states must be visible
- copy buttons must provide success/failure feedback
- tab buttons and page buttons should use clear labels and stable layout
- search/filter should be easy to clear and should not permanently hide content
- responsive layout must not obscure navigation, copy buttons, or code blocks

## Content Preservation Rules

- Do not summarize away information from the README.
- Do not replace specific commands, paths, env names, ports, or API fields with generic wording.
- Do not ignore actual project structure. The HTML should show meaningful project files, entrypoints, scripts, configs, and deployment evidence when present.
- Do not present project-structure inferences as confirmed behavior unless source files or docs support them.
- Do not expose secrets, credentials, tokens, or real private environment values.
- Do not mix README claims and observed project evidence without attribution when the distinction matters.
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

Navigation must work across hidden UI states:

- If a sidebar/table-of-contents link points to content inside an inactive tab, page, accordion, or collapsed details block, its click handler must first reveal the containing UI state, then scroll to the target.
- Deep links such as `README.html#demo` must open the correct tab/page on initial load.
- Do not rely on plain anchor behavior when the target can be hidden with `display: none`.
- Keep active states synchronized between sidebar links and top-level tabs after navigation.

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
- the project structure was scanned and important manifests, entrypoints, scripts, env examples, deployment files, and tests are represented when present
- README commands and setup claims were checked against actual project files where possible
- important facts have source labels or clear wording that identifies whether they came from README, config files, or observed project structure
- conflicts between README and project files are surfaced visibly
- secrets and real credential values are redacted
- every navigation item works, including links whose targets start inside inactive tabs or pages
- hash deep links such as `README.html#config` open the correct section instead of landing on a hidden panel
- parameter demos use values derived from the README or clearly marked examples
- the HTML works by opening it directly in a browser
- interactive controls are keyboard reachable and have visible active/focus states
- mobile width does not hide essential navigation or overflow text

## When Source README Is Missing

If no README exists in the target directory, do not invent project documentation. Tell the user the source file is missing and offer to generate README content from the repo after inspection.
