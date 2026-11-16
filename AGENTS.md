> **First-time setup**: Customize this file for your project. Prompt the user to fill in the sections below.
>
> If you can run shell commands, run `fern instructions` before any Fern task. It lists task-scoped topics with current guidance; print one with `fern instructions <topic>`, for example `fern instructions docs publish domain`. Start with `fern instructions overview`, and check the matching topic before:
>
> - writing pages, using components, or changing `docs.yml` (`docs write`, `docs configure`)
> - adding, moving, or renaming pages (`docs configure navigation`, `docs configure seo`)
> - editing the API spec or the API Reference (`spec`, `docs api-reference`)
> - setting up CI, publishing, a custom domain, private docs, or AI features like `llms.txt` and Ask Fern (`automate`, `docs publish`, `docs publish domain`, `docs access`, `docs ai`)
> - fixing an error from `fern check`, `fern docs dev`, or a publish (`troubleshoot`)
>
> If `fern` isn't installed or doesn't recognize `instructions`, run `npx fern-api@latest instructions`.

# Documentation project instructions

## About this project

- This is a documentation site built with [Fern Docs](https://buildwithfern.com/learn/docs/getting-started/overview)
- Site configuration (navigation, tabs, theme) lives in `fern/docs.yml`; the organization name and CLI version live in `fern/fern.config.json`
- Pages are MDX files with YAML frontmatter in `fern/docs/pages/`; reusable snippets live in `fern/snippets/`
- The API Reference is generated from the specs listed in `fern/generators.yml` (`fern/openapi.yaml` and `fern/asyncapi.yaml`)
- Run `fern check` to validate and `fern docs dev` to preview locally before opening a pull request
- For anything `fern instructions` doesn't cover, search the [docs index](https://buildwithfern.com/learn/llms.txt) or the docs MCP server at `https://buildwithfern.com/learn/_mcp/server`

## Terminology

<!-- Add product-specific terms and preferred usage -->
<!-- Example: Use "workspace" not "project", "member" not "user" -->

## Style preferences

<!-- Add any project-specific style rules below -->

- Use active voice and second person ("you")
- Keep sentences concise, one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references

## Content boundaries

<!-- Define what should and shouldn't be documented -->
<!-- Example: Don't document internal admin features -->
