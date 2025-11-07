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

</div>

## Customer Showcase

Get inspired by API documentation built with Fern: [Webflow](https://developers.webflow.com) | [Cartesia](https://docs.cartesia.ai) | [Cohere](https://docs.cohere.com) | [ElevenLabs](https://elevenlabs.io/docs)

---

## Requirements

- Node 18 or higher
- A [GitHub](https://github.com) account
- Knowledge of the command line

### Step 1: Use this template

1. Click on the **Use this template** button (found at the top right of this page). You must be logged into GitHub.
2. Choose the option to **create a new repository**. Name it `fern-docs`.
3. Install the Fern Command Line Interface (CLI) by running:

```bash
npm install -g fern-api
```

### Step 2: Clone and open the repo in your preferred code editor

Clone your newly created repository and open it in your favorite code editor (e.g., Cursor, VS Code).

The files and folders discussed in the following steps will be inside the `fern/` folder in your repository.

### Step 3: Customize your organization name

You need to replace `"plantstore"` with your own organization name in two files:

**1. Update `fern.config.json`:**
Open the `fern.config.json` file and change the organization name:

```json
{
  "organization": "your-company-name",
  "version": "0.84.1"
}
```

Run the following command to ensure you are using the latest version of Fern:

```bash
fern upgrade
```

Replace `plantstore` with your own organization's name. Use only alphanumeric characters, hyphens, and underscores. 

**2. Update `docs.yml`:**
Open the `docs.yml` file and change the `instances.url` value from `plantstore` to your company name that you used for the `organization` name. **Do not use spaces and leave the rest of the URL (`docs.buildwithfern.com`) unchanged.**

It should now read:

```yml
instances:
  - url: your-company-name.docs.buildwithfern.com
```

### Step 4: Generate your documentation

Run the following command:

```bash
fern generate --docs
```

You will be prompted to log in and connect your GitHub account. 

You might also be prompted, `yes` or `no`, about if you want to proceed with generating docs and informed that you can choose between using the `--preview` flag or not. You can choose to use either `fern generate --docs` or `fern generate --docs --preview` at this time. This decision is important later, when you are making changes that might affect a production docs environment, but it won't impact your docs project now.

Once the documentation is generated, you will receive the URL where your documentation is published. For example:

```shell
┌─
│ ✓  your-company-name.docs.buildwithfern.com
└─
```

### Step 5: Try local development

Preview your documentation locally. Run ​`fern docs dev`​ to access your docs on your local server at port 3000, hot-reloading as you edit your markdown and OpenAPI files. [Learn more](https://buildwithfern.com/learn/docs/getting-started/development?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=step6) or [watch a 10-second demo](https://www.loom.com/share/0a4658bd78cb45d5a9519277852c7a24?sid=3ce69ad0-bfdb-4fa1-9abf-2f4366d084b9).

### Step 6: Preview your documentation
You can generate documentation previews

#### Generate previews from CLI

To preview updates to your documentation before publishing changes, run `fern generate --docs --preview`.

#### Configure PR previews

Your quickstart Fern project also includes GitHub Actions, including an action that enables generating previews in PRs. You don't need to update anything in the GitHub actions, but you do need to create a `FERN_TOKEN` auth token to enable them.

1. Open your GitHub repository and [create a new repository secret](https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets#creating-secrets-for-a-repository).
2. For the **Name**, use `FERN_TOKEN`.
3. In your local terminal, run [`fern token`](https://buildwithfern.com/learn/cli-api-reference/cli-reference/commands#detailed-command-documentation) to generate an auth token value.
4. Copy the output from your terminal, and paste in GitHub as the **Value**.
5. Save your new secret.

You might need to re-run preview builds for any PRs that were opened before you configured the `FERN_TOKEN`.

For more information about built-in automation for previews and the `preview-docs.yml` GitHub action, see the [Previewing changes in a PR](https://buildwithfern.com/learn/docs/preview-publish/previewing-changes-in-a-pr#usage-in-github-actions) Fern docs.

### Step 7: Customize your documentation

You must run `fern generate --docs` after any modifications to re-generate and publish your documentation site.

To use your own OpenAPI specification file or to update the existing one:

- Update or replace the OpenAPI specification file in the `openapi/` folder.
- _Note: Don't have an OpenAPI spec? Use Fern's simpler format to define your API._ [_Learn more_](https://github.com/fern-api/docs-starter-fern-definition?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=step7).

To modify the other docs pages:

- Update the Markdown files located in the `docs/pages/` folder, such as `welcome.mdx`.

To modify site styles and navigation, or to add new pages:

- See [Writing Content](https://buildwithfern.com/learn/docs/content/write-markdown?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=step7).

To learn about Fern's built-in component library you can use within MDX files:

- See the [Component Library](https://buildwithfern.com/learn/docs/content/components/overview?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=step7).

### Step 7: Set up a custom domain

If you wish to use a custom subdomain like `https://docs.YOUR_ORGANIZATION.com` or a subpath like `https://YOUR_ORGANIZATION.com/docs`, you can subscribe to the [Starter plan](https://buildwithfern.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=step8). Once subscribed, update `docs.yml` with the custom domain configuration:

```yaml
- url: plantstore.docs.buildwithfern.com
  custom-domain: plantstore.dev
```

### Step 8: Explore advanced features

For advanced documentation features and options, view the full [project structure](https://buildwithfern.com/learn/docs/getting-started/project-structure?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=step9).

Good luck creating beautiful and functional documentation! 🌿

---

## Support

Need help? [Set up a call](https://buildwithfern.com/contact?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=support) with an expert or email us at [support@buildwithfern.com](mailto:support@buildwithfern.com).
