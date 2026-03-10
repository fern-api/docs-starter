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

# Docs starter

Create beautiful documentation in under 5 minutes using your OpenAPI specification.

</div>

## Customer showcase

Get inspired by API documentation built with Fern: [Webflow](https://developers.webflow.com) | [You.com](https://you.com/docs) | [Cohere](https://docs.cohere.com) | [ElevenLabs](https://elevenlabs.io/docs)

---

## Requirements

- Node 18 or higher
- A [GitHub](https://github.com) account
- Knowledge of the command line

## Getting started

> **Prefer a no-code setup?** Use the [guided UI](https://dashboard.buildwithfern.com/get-started) to get started from your browser instead.

Follow the steps below, or see the [Docs quickstart](https://buildwithfern.com/learn/docs/getting-started/quickstart) for a more detailed walkthrough.

1. **Install the CLI**

   ```bash
   npm install -g fern-api
   ```

2. **Initialize your docs**

   Clone this starter template, or run `fern init --docs` to start from scratch.

3. **Configure your organization**

   Set your organization name in `fern.config.json` and your docs URL in `docs.yml`:

   ```json
   // fern.config.json
   { "organization": "your-org-name", "version": "4.21.3" }
   ```

   ```yaml
   # docs.yml
   instances:
     - url: your-org-name.docs.buildwithfern.com
   ```

4. **Preview locally**

   ```bash
   fern docs dev
   ```

5. **Publish**

   ```bash
   fern generate --docs
   ```

## Customize your docs

Once you're up and running, you can tailor your docs site to match your brand and product:

- **[Brand your docs](https://buildwithfern.com/learn/docs/configuration/site-level-settings)** — Set custom colors, logo, favicon, and fonts in `docs.yml`
- **[Add an API reference](https://buildwithfern.com/learn/docs/api-references/generate-api-ref)** — Auto-generate interactive API docs from your OpenAPI spec
- **[Use components](https://buildwithfern.com/learn/docs/writing-content/components/overview)** — Tabs, accordions, callouts, cards, and more out of the box
- **[Set up a custom domain](https://buildwithfern.com/learn/docs/preview-publish/setting-up-your-domain)** — Host on your own domain (e.g., `docs.example.com`)
- **[Configure analytics](https://buildwithfern.com/learn/docs/integrations/overview)** — Integrate with PostHog, Segment, Google Tag Manager, and others
- **[Customize navigation](https://buildwithfern.com/learn/docs/configuration/navigation)** — Add versioned docs, tabs, nested sections, and multi-product layouts

---

## Support

Need help? [Set up a call](https://buildwithfern.com/contact?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=support) with an expert or email us at [support@buildwithfern.com](mailto:support@buildwithfern.com).
