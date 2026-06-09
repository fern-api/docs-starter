<br/>

<div align="center">
  <a href="https://www.buildwithfern.com/?utm_source=github&utm_medium=readme&utm_campaign=fern&utm_content=logo">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="/fern/docs/assets/fern-logo-white.svg">
      <source media="(prefers-color-scheme: light)" srcset="/fern/docs/assets/fern-logo-primary.svg">
      <img alt="logo" src="/fern/docs/assets/fern-logo-primary.svg" height="50" align="center">
    </picture>
  </a>
  
  <br/>

# Docs Starter

Create beautiful documentation in under 5 minutes using your OpenAPI specification.

[![View live example](https://img.shields.io/badge/View-Live_Example-green?style=flat)](https://plantstore.docs.buildwithfern.com)

</div>

## Customer showcase

Get inspired by API documentation built with Fern: [Webflow](https://developers.webflow.com) | [You.com](https://you.com/docs) | [Cohere](https://docs.cohere.com) | [ElevenLabs](https://elevenlabs.io/docs)

---

## Requirements

- **Node.js 18+** (required for `npm install`) _or_ **Homebrew** (macOS/Linux)
- A [GitHub](https://github.com) account
- A [Fern](https://buildwithfern.com) account (free to start)

## Installation

Install the Fern CLI globally using one of the following methods:

**npm** (all platforms):

```bash
npm install -g fern-api
```

**Homebrew** (macOS / Linux):

```bash
brew install fern-api
```

Verify the installation:

```bash
fern --version
```

## Repository structure

```
fern/
├── docs.yml              # Site config: navigation, theme, tabs, navbar links
├── fern.config.json      # Organization name and CLI version
├── generators.yml        # API spec sources (OpenAPI, AsyncAPI)
├── openapi.yaml          # Sample Plant Store OpenAPI spec
├── asyncapi.yaml         # Sample AsyncAPI spec
├── styles.css            # Custom CSS overrides
├── snippets/             # Reusable MDX content fragments
├── docs/
│   ├── pages/            # Markdown (MDX) documentation pages
│   ├── assets/           # Logos, favicon, and static assets
│   └── changelog/        # Changelog entries
└── ...
.github/
└── workflows/
    ├── check.yml         # Validates your API spec on every PR and push
    ├── preview-docs.yml  # Generates a preview URL on every PR
    └── publish-docs.yml  # Publishes docs to production on merge to main
```

## Getting started

> **Prefer a no-code setup?** Use the [guided UI](https://dashboard.buildwithfern.com/get-started) to get started from your browser instead.

### 1. Create your repository

Use this template to create a new repository:

```bash
# Using the GitHub CLI
gh repo create my-org/my-docs --template fern-api/docs-starter --private --clone
cd my-docs
```

Or click **"Use this template"** on [GitHub](https://github.com/fern-api/docs-starter) and clone the resulting repository.

Alternatively, start from scratch in any directory:

```bash
fern init --docs
```

> **Note:** `fern init --docs` generates only `docs.yml` and `fern.config.json`. You'll need to add your own pages and API spec afterward.

### 2. Configure your organization

Update `fern/fern.config.json` with your organization name:

```json
{
  "organization": "your-org-name",
  "version": "5.35.4"
}
```

Update the docs URL in `fern/docs.yml`:

```yaml
instances:
  - url: your-org-name.docs.buildwithfern.com
```

Use only alphanumeric characters, hyphens, and underscores for both values.

### 3. Validate your configuration

Run the linter to catch errors before previewing:

```bash
fern check
```

### 4. Preview locally

Start a local development server with hot-reloading:

```bash
fern docs dev
```

Open [http://localhost:3000](http://localhost:3000) to see your docs. Changes to MDX files and `docs.yml` will reload automatically.

### 5. Publish

When you're ready to go live:

```bash
fern generate --docs
```

This requires a `FERN_TOKEN`. Get yours from the [Fern dashboard](https://dashboard.buildwithfern.com) under **Settings > API keys**.

To generate a shareable preview URL without publishing:

```bash
fern generate --docs --preview
```

## CI/CD workflows

This template includes three GitHub Actions workflows out of the box:

| Workflow | Trigger | What it does |
|----------|---------|--------------|
| `check.yml` | Every PR and push to `main` | Runs `fern check` to validate your API spec |
| `preview-docs.yml` | Every PR | Generates a preview URL and posts it as a PR comment |
| `publish-docs.yml` | Push to `main` (after first build) | Publishes your docs to production |

### Setting up CI

Add your `FERN_TOKEN` as a repository secret:

1. Go to **Settings > Secrets and variables > Actions** in your GitHub repository.
2. Click **New repository secret**.
3. Name it `FERN_TOKEN` and paste your token value.

The `check.yml` workflow works without a token; only preview and publish require it.

## Customize your docs

Once you're up and running, tailor your docs to match your brand and product:

- **[Brand your docs](https://buildwithfern.com/learn/docs/configuration/site-level-settings)** — Set custom colors, logo, favicon, and fonts in `docs.yml`
- **[Add an API reference](https://buildwithfern.com/learn/docs/api-references/generate-api-ref)** — Auto-generate interactive API docs from your OpenAPI spec
- **[Use components](https://buildwithfern.com/learn/docs/writing-content/components/overview)** — Tabs, accordions, callouts, cards, and more out of the box
- **[Set up a custom domain](https://buildwithfern.com/learn/docs/preview-publish/setting-up-your-domain)** — Host on your own domain (e.g., `docs.example.com`)
- **[Configure analytics](https://buildwithfern.com/learn/docs/integrations/overview)** — Integrate with PostHog, Segment, Google Tag Manager, and others
- **[Customize navigation](https://buildwithfern.com/learn/docs/configuration/navigation)** — Add versioned docs, tabs, nested sections, and multi-product layouts

## Useful commands

| Command | Description |
|---------|-------------|
| `fern check` | Validate your Fern configuration and API specs |
| `fern docs dev` | Start local dev server with hot-reloading |
| `fern generate --docs` | Publish docs to your configured URL |
| `fern generate --docs --preview` | Generate a shareable preview URL |
| `fern upgrade` | Upgrade the CLI version in `fern.config.json` |

## Further reading

- [Docs quickstart](https://buildwithfern.com/learn/docs/getting-started/quickstart)
- [CLI reference](https://buildwithfern.com/learn/cli-api-reference/cli-reference/overview)
- [Writing content (Markdown)](https://buildwithfern.com/learn/docs/writing-content/overview)
- [Configuration reference](https://buildwithfern.com/learn/docs/configuration/overview)

---

## Support

Need help? [Set up a call](https://buildwithfern.com/contact?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=support) with an expert or email us at [support@buildwithfern.com](mailto:support@buildwithfern.com).
