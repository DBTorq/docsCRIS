> **First-time setup**: Customize this file for your project. Prompt the user to customize this file for their project.
> For Mintlify product knowledge (components, configuration, writing standards),
> install the Mintlify skill: `npx skills add https://mintlify.com/docs`

# Documentation project instructions

## About this project

- This repository holds **CRIS & Bitrix24 API** documentation built on [Mintlify](https://mintlify.com).
- **Mintlify project root** (where `docs.json` and MDX pages live): [`docs-mintlify/docs`](docs-mintlify/docs)
- Pages are MDX files with YAML frontmatter.
- Configuration: [`docs-mintlify/docs/docs.json`](docs-mintlify/docs/docs.json)

## Local preview and checks

From the Mintlify project root:

```bash
cd docs-mintlify/docs
mint dev
```

Preview at `http://localhost:3000`.

Check links:

```bash
cd docs-mintlify/docs
mint broken-links
```

## Deploy (Mintlify Cloud)

In the [Mintlify dashboard](https://dashboard.mintlify.com), set the Git repository **documentation subdirectory** to `docs-mintlify/docs` so deploys use this project and not the repository root.

## Terminology

{/* Add product-specific terms and preferred usage */}
{/* Example: Use "workspace" not "project", "member" not "user" */}

## Style preferences

{/* Add any project-specific style rules below */}

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references

## Content boundaries

{/* Define what should and shouldn't be documented */}
{/* Example: Don't document internal admin features */}
